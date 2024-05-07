# Ubuntu 22.04 安装 AFL 及 Qemu Mode 实践

Ubuntu 22.04 LTS 64位系统安装 American Fuzzy Lop (AFL) 2.56b 踩坑记录，使用 QEMU mode 进行简单测试实践。

&lt;!--more--&gt;

## 安装依赖
```bash
sudo apt update
sudo apt-get install -y cargo \
						python2 \
                        cmake \
                        g&#43;&#43; \
                        git \
                        bison \
                        libz3-dev  \
                        ninja-build \
                        python3-pip \
                        zlib1g-dev
pip3 install lit
```
### 添加环境变量 Path
编辑终端配置文件。
```
# bash
sudo nano ~/.bashrc

# zsh
sudo nano ~/zshrc
```

添加环境变量：
```bash
export PATH=${HOME}/.local/bin:${PATH}
```

![编辑Path变量](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202401071608420.png)

启用配置文件，**bash** 使用`source ~/.bashrc`；**zsh** 使用`~/.zshrc`。
### 设置 Python
AFL 使用的是 Python2，Ubuntu22.04 上没有安装。因此需要安装 Python2并将其设置为默认 Python。
```bash
sudo ln -s /usr/bin/python2 /usr/bin/python
```

### 安装 clang10
参考此文章安装并设置 `clang10` 为默认版本。

{{&lt; link &#34;https://www.haoyep.com/posts/ubuntu22-install-clang10/&#34; &#34;Ubuntu 22.04 LTS 64位系统安装 clang10 版本&#34; &#34;Ubuntu 22.04 LTS 64位系统安装 clang10 版本&#34; true &gt;}}

## 安装 Z3
要求版本号大于4.5
```bash
git clone https://github.com/Z3Prover/z3.git
cd z3 &amp;&amp; mkdir build &amp;&amp; cd build
cmake -G &#34;Ninja&#34; ../
ninja
```

{{&lt; admonition warning &#34;Git Clone错误解决方案&#34; &gt;}}
- **执行 git clone 报错**：
`fatal: unable to access &#39; https://github.com/Z3Prover/z3/ &#39;: GnuTLS recv error (-110): The TLS connection was non-properly terminated.`

- **解决方案**

```bash
sudo apt-get update
sudo apt-get install gnutls-bin
git config --global http.sslVerify false
git config --global http.postBuffer 1048576000
```

到此问题解决，重新进行`git clone`，可以顺畅下载。
{{&lt; /admonition &gt;}}

## 安装 AFL
```bash
git clone -b v2.56b https://github.com/google/AFL.git afl
cd afl &amp;&amp; make
```
![afl工具列表](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202312132214349.png)

### 安装 qemu 模式
编译 qemu，支持二进制文件黑盒分析。
#### 依赖环境
安装 libtool 等资源库
```bash
sudo apt-get install libtool-bin libgtk2.0-dev -y
```

#### patch 代码
为了避免 [AFL/issues/41](https://github.com/google/AFL/issues/41) 中出现的`error: ‘SIOCGSTAMP’ undeclared here (not in a function); did you mean ‘SIOCSRARP’?`、`error: ‘SIOCGSTAMPNS’ undeclared here (not in a function); did you mean ‘SIOCGSTAMP_OLD’?`，需要修改为 [patch](https://github.com/Mindavi/AFL/blob/6c917e3d63a2a0685d58c3518524f9615b001893/qemu_mode/patches/syscall.diff) 中的文件内容。修改 `afl/qemu_mode/patches`目录中的`syscall.diff`文件内容如下：
```
--- qemu-2.10.0-clean/linux-user/syscall.c	2020-03-12 18:47:47.898592169 &#43;0100
&#43;&#43;&#43; qemu-2.10.0/linux-user/syscall.c	2020-03-12 19:16:41.563074307 &#43;0100
@@ -34,6 &#43;34,7 @@
 #include &lt;sys/resource.h&gt;
 #include &lt;sys/swap.h&gt;
 #include &lt;linux/capability.h&gt;
&#43;#include &lt;linux/sockios.h&gt; // https://lkml.org/lkml/2019/6/3/988
 #include &lt;sched.h&gt;
 #include &lt;sys/timex.h&gt;
 #ifdef __ia64__
@@ -116,6 &#43;117,8 @@ int __clone2(int (*fn)(void *), void *ch
 
 #include &#34;qemu.h&#34;
 
&#43;extern unsigned int afl_forksrv_pid;
&#43;
 #ifndef CLONE_IO
 #define CLONE_IO                0x80000000      /* Clone io context */
 #endif
@@ -256,7 &#43;259,9 @@ static type name (type1 arg1,type2 arg2,
 #endif
 
 #ifdef __NR_gettid
-_syscall0(int, gettid)
&#43;// taken from https://patchwork.kernel.org/patch/10862231/
&#43;#define __NR_sys_gettid __NR_gettid
&#43;_syscall0(int, sys_gettid)
 #else
 /* This is a replacement for the host gettid() and must return a host
    errno. */
@@ -6219,7 &#43;6224,8 @@ static void *clone_func(void *arg)
     cpu = ENV_GET_CPU(env);
     thread_cpu = cpu;
     ts = (TaskState *)cpu-&gt;opaque;
-    info-&gt;tid = gettid();
&#43;    // taken from https://patchwork.kernel.org/patch/10862231/
&#43;    info-&gt;tid = sys_gettid();
     task_settid(ts);
     if (info-&gt;child_tidptr)
         put_user_u32(info-&gt;tid, info-&gt;child_tidptr);
@@ -6363,9 &#43;6369,11 @@ static int do_fork(CPUArchState *env, un
                mapping.  We can&#39;t repeat the spinlock hack used above because
                the child process gets its own copy of the lock.  */
             if (flags &amp; CLONE_CHILD_SETTID)
-                put_user_u32(gettid(), child_tidptr);
&#43;                // taken from https://patchwork.kernel.org/patch/10862231/
&#43;                put_user_u32(sys_gettid(), child_tidptr);
             if (flags &amp; CLONE_PARENT_SETTID)
-                put_user_u32(gettid(), parent_tidptr);
&#43;                // taken from https://patchwork.kernel.org/patch/10862231/
&#43;                put_user_u32(sys_gettid(), parent_tidptr);
             ts = (TaskState *)cpu-&gt;opaque;
             if (flags &amp; CLONE_SETTLS)
                 cpu_set_tls (env, newtls);
@@ -11402,7 &#43;11410,8 @@ abi_long do_syscall(void *cpu_env, int n
         break;
 #endif
     case TARGET_NR_gettid:
-        ret = get_errno(gettid());
&#43;        // taken from https://patchwork.kernel.org/patch/10862231/
&#43;        ret = get_errno(sys_gettid());
         break;
 #ifdef TARGET_NR_readahead
     case TARGET_NR_readahead:
@@ -11688,8 &#43;11697,20 @@ abi_long do_syscall(void *cpu_env, int n
         break;
 
     case TARGET_NR_tgkill:
-        ret = get_errno(safe_tgkill((int)arg1, (int)arg2,
-                        target_to_host_signal(arg3)));
&#43;        {
&#43;          int pid  = (int)arg1,
&#43;              tgid = (int)arg2,
&#43;              sig  = (int)arg3;
&#43;
&#43;          /* Not entirely sure if the below is correct for all architectures. */
&#43;
&#43;          if(afl_forksrv_pid &amp;&amp; afl_forksrv_pid == pid &amp;&amp; sig == SIGABRT)
&#43;              pid = tgid = getpid();
&#43;
&#43;          ret = get_errno(safe_tgkill(pid, tgid, target_to_host_signal(sig)));
&#43;
&#43;        }
&#43;
         break;
 
 #ifdef TARGET_NR_set_robust_list
```
![替换syscall.diff文件内容](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202312132314613.png)

在 `afl/qemu_mode/patches`目录中新增`memfd_create.diff`文件，内容如下：
```
diff -ru qemu-2.10.0-clean/util/memfd.c qemu-2.10.0/util/memfd.c
--- qemu-2.10.0-clean/util/memfd.c      2018-11-20 18:11:00.170271506 &#43;0100
&#43;&#43;&#43; qemu-2.10.0/util/memfd.c    2018-11-20 18:11:13.398423613 &#43;0100
@@ -37,7 &#43;37,7 @@
 #include &lt;sys/syscall.h&gt;
 #include &lt;asm/unistd.h&gt;
 
-static int memfd_create(const char *name, unsigned int flags)
&#43;int memfd_create(const char *name, unsigned int flags)
 {
 #ifdef __NR_memfd_create
     return syscall(__NR_memfd_create, name, flags);
```
![新增memfd_create.diff文件](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202312132253824.png)
#### 修改脚本
修改`build_qemu_support.sh`文件
1. 修改`QEMU_URL`为`QEMU_URL=&#34;https://download.qemu.org/qemu-${VERSION}.tar.xz&#34;`
![修改QEMU_URL](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202312132254858.png)
2. 在`patch -p1 &lt;../patches/syscall.diff || exit 1`的下一行添加`patch -p1 &lt;../patches/memfd_create.diff || exit 1`
![添加memfd_create.diff patch命令](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202312132255894.png)
#### 编译及安装
在 afl 的根目录打开终端执行以下命令：
```text
cd qemu_mode

./build_qemu_support.sh

cd ..
sudo make install
```

![afl编译成功示例](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202312132316017.png)
### 运行 qemu mode
假设存在文件目录结构如下。其中`in`文件夹中的`a.in`文件是输入的初始种子，手动输入一个命令行参数进去即可。
```bash
./qemu-test/
├── benchmark /* 要测试的程序二进制文件 */
├── in        /* 输入文件夹，存储用户自定义的输入种子 */
│   └── a.in
└── out       /* 输出文件夹，存储AFL探索到的测试用例 */
```

则使用以下命令运行 AFL qemu mode。稍等片刻，就可以看到 AFL 运行界面。
```bash
afl-fuzz -i in/ -o out/ -Q ./benchmark
```
![运行 qemu mode](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/run-afl-qemu-mode.png)
#### 停止运行
当`cycles done`的数字变成绿色，说明 AFL 已找不到更有价值的路径。此时，就可以按下`Ctrl&#43;C`终止 AFL 运行。
![绿色，可以停止运行AFL](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202312221256348.png)

## 失败报错解决方案
### core_pattern
![core_pattern错误](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202312141514236.png)

参考 [AFL fuzzing without root - avoid modifying /proc/sys/kernel/core_pattern](https://stackoverflow.com/questions/35441062/afl-fuzzing-without-root-avoid-modifying-proc-sys-kernel-core-pattern)，这是因为 AFL 希望系统将 coredump 输出到文件，而不是上报给系统的处理程序。报错信息如下：
{{&lt; admonition failure &#34;core dump报错&#34; &gt;}}
[-] Hmm, your system is configured to send core dump notifications to an
    external utility. This will cause issues: there will be an extended delay
    between stumbling upon a crash and having this information relayed to the
    fuzzer via the standard waitpid() API.

    To avoid having crashes misinterpreted as timeouts, please log in as root
    and temporarily modify /proc/sys/kernel/core_pattern, like so:

    echo core &gt;/proc/sys/kernel/core_pattern

[-] PROGRAM ABORT : Pipe at the beginning of &#39;core_pattern&#39;
         Location : check_crash_handling(), afl-fuzz.c:7314
{{&lt; /admonition &gt;}}

解决方法有两种：
1. 添加环境变量，参考 [Disabling the /proc/sys/kernel/core_pattern check](https://groups.google.com/g/afl-users/c/7arn66RyNfg/m/BsnOPViuCAAJ?pli=1)
```bash
export AFL_I_DONT_CARE_ABOUT_MISSING_CRASHES=1
```

{{&lt; admonition &gt;}}
按照之前 [stackoverflow问题](https://stackoverflow.com/questions/35441062/afl-fuzzing-without-root-avoid-modifying-proc-sys-kernel-core-pattern)中的评论，这个环境变量只是抑制了有关它的警告？使用此标志，AFL 将运行并且不会显示警告消息，并[可能错过崩溃](https://github.com/google/fuzzer-test-suite/issues/60)。
{{&lt; /admonition &gt;}}

2. 按照 AFL 提示修改文件
```bash
sudo su
echo core &gt;/proc/sys/kernel/core_pattern
```
### CPU frequency
![CPU frequency错误](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202312141515270.png)
报错信息如下：
{{&lt; admonition failure &#34;core dump报错&#34; &gt;}}
[-] Whoops, your system uses on-demand CPU frequency scaling, adjusted
    between 781 and 1660 MHz. Unfortunately, the scaling algorithm in the
    kernel is imperfect and can miss the short-lived processes spawned by
    afl-fuzz. To keep things moving, run these commands as root:

    cd /sys/devices/system/cpu
    echo performance | tee cpu*/cpufreq/scaling_governor

    You can later go back to the original state by replacing &#39;performance&#39; with
    &#39;ondemand&#39;. If you don&#39;t want to change the settings, set AFL_SKIP_CPUFREQ
    to make afl-fuzz skip this check - but expect some performance drop.

[-] PROGRAM ABORT : Suboptimal CPU scaling governor
         Location : check_cpu_governor(), afl-fuzz.c:7376
{{&lt; /admonition &gt;}}
这是 CPU 频率未固定的错误提示，参考[这里](http://www.cse.psu.edu/~gxt29/teaching/cs447s19/slides/06testingFuzzing.pdf)，解决方案是引入环境变量：
```bash
export AFL_SKIP_CPUFREQ=1
```

---

> 作者: [云吱](https://www.haoyep.com/)  
> URL: https://www.haoyep.com/posts/afl-install/  


# Ubuntu 22.04 LTS 64位系统安装 clang10 版本

本文记录了Ubuntu 22.04 LTS 64位系统安装 clang10 版本的过程。

&lt;!--more--&gt;

## 安装 clang10
1. 编辑 apt 源文件。
```bash
sudo nano /etc/apt/sources.list
```

添加以下内容：
```
# clang 9/10
# i386 not available
deb http://apt.llvm.org/focal/ llvm-toolchain-focal main
deb-src http://apt.llvm.org/focal/ llvm-toolchain-focal main
# 9
deb http://apt.llvm.org/focal/ llvm-toolchain-focal-9 main
deb-src http://apt.llvm.org/focal/ llvm-toolchain-focal-9 main
# 10
deb http://apt.llvm.org/focal/ llvm-toolchain-focal-10 main
deb-src http://apt.llvm.org/focal/ llvm-toolchain-focal-10 main
```
![添加clang9/10源](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202401171506785.png)

2. 安装 clang10
```bash
# 先添加key
wget -O - https://apt.llvm.org/llvm-snapshot.gpg.key | sudo apt-key add -
# 更新源
sudo apt update
# 安装 clang10
sudo apt-get install clang-10 llvm-10-dev llvm-10-tools -y
```

## 切换默认命令版本
安装完成后，默认的命令是`clang-10`和`clang&#43;&#43;-10`，需要使用`update-alternatives`来设置成`clang`和`clang&#43;&#43;`。

首先查看当前 clang 默认版本：
```bash
clang  --version
```
如图，当前版本是 clang14
![clang 默认版本输出](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202401171507177.png)

### 切换成 clang10
```bash
sudo update-alternatives --install /usr/bin/clang clang /usr/bin/clang-10 1 --slave /usr/bin/clang&#43;&#43; clang&#43;&#43; /usr/bin/clang&#43;&#43;-10
```
![切换成 clang10](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202401171507032.png)

### 恢复原有的 clang 版本
这里也给出切换回 clang14的命令：
```bash
sudo update-alternatives --install /usr/bin/clang clang /usr/bin/clang-14 2 --slave /usr/bin/clang&#43;&#43; clang&#43;&#43; /usr/bin/clang&#43;&#43;-14
```

---

> 作者: [云吱](https://www.haoyep.com/)  
> URL: https://www.haoyep.com/posts/ubuntu22-install-clang10/  


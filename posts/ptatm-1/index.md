# PTATM（一）：初始化工作

本文介绍适用于多路径任务的多核系统pWCET分析工具——PTATM的初始化工作，如内核、环境变量等。
&lt;!--more--&gt;

本文介绍 [PTATM](https://github.com/panzhenyu/PTATM) 的初始化工作，如内核、环境变量等。
{{&lt; admonition info &#34;PTATM简介&#34; &gt;}}
[PTATM](https://github.com/panzhenyu/PTATM)结合了多路径任务分段方法、共享Cache竞争下的任务段信息收集方法以及分段任务的pWCET分布生成方法，是一种适用于多路径任务的多核系统pWCET分析工具。
{{&lt; /admonition &gt;}}

## 系统环境
[PTATM](https://github.com/panzhenyu/PTATM) 开发时的环境为：

| 环境 | 配置 |
| :----: | :----: |
| 操作系统 | Ubuntu 22.04 |
| 内核版本 | 5.19.0-32-generic |

因此，理论上只要是`5.19.0-x`内核版本的 Ubuntu22.04 即可。使用`uname -r`命令可以查看当前系统版本号。下图表示当前系统的内核的版本是`5.19.0-50-generic`，满足运行条件，可以跳过本节系统环境配置。
![image.png](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311181922930.png)
### 查看系统已安装内核
```bash
dpkg --get-selections | grep linux-image | grep -v deinstall
```
使用上面的命令查看系统已经安装的所有内核版本。如果有`5.19.0-x`内核版本，跳到[1.3 更新 grub](#13-更新grub)。
![image.png](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311181930258.png)
### 更换 Linux 内核
如果内核版本不是`5.19.0-x`，则需要更换内核。使用下面的命令查看可以安装的内核版本。
```bash
apt-cache search linux-image-5.19.* | grep generic
```

![image.png](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311181942023.png)
选择图中最后一个内核版本`linux-image-5.19.0-50-generic`安装：
```bash
sudo apt-get install linux-image-5.19.0-50-generic
sudo apt-get install linux-headers-5.19.0-50-generic linux-modules-extra-5.19.0-50-generic
```
如果要安装其他版本的内核，记得把上面命令中的`5.19.0-50-generic`改成对应的版本。
### 更新`grub`
还是假设要更换到`5.19.0-50-generic`内核版本。
```bash
# 将 5.19.0-50-generic 替换你需要的version
sudo update-initramfs -u -k 5.19.0-50-generic
```
修改 grub 使`5.19.0-50-generic`为默认启动项
```bash
sudo nano /etc/default/grub
```
将`GRUB_DEFAULT`一项修改为：
```bash
&#34;Advanced options for Ubuntu&gt;Ubuntu, with Linux 5.19.0-50-generic&#34;
```
{{&lt; admonition tip &#34;同理，记得把`5.19.0-50-generic`替换你需要的 version&#34; false &gt;}}
{{&lt; /admonition &gt;}}

![image.png](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311181952427.png)

更新 grub，然后重启。查看内核版本是否切换成功。
```bash
# 更新 grub
sudo update-grub
# 重启
sudo reboot
# 查看当前内核版本
uname -r
```

## 安装 perf
使用下面的命令安装当前内核版本的 `perf`：
```bash
sudo apt-get install linux-tools-common -y
sudo apt-get install linux-tools-&#34;$(uname -r)&#34; -y
sudo apt-get install linux-cloud-tools-&#34;$(uname -r)&#34; -y
sudo apt-get install linux-tools-generic -y
sudo apt-get install linux-cloud-tools-generic -y
```

## Python 环境
使用 Python3，运行时如果发现有依赖包没安装，自行使用`pip3 install &lt;module&gt;`安装缺少的依赖包。

## 环境变量
在`PTATM`的本地文件夹中打开终端，输入`pwd`查看当前目录位置：
![image.png](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311182000356.png)

之后，每次需要运行`PTATM`时，先在终端导入这个环境变量：
```bash
export PTATM=/home/pzy/project/PTATM_backup
```

![设置PTATM目录](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311182038059.png)

---

> 作者: [云吱](https://www.haoyep.com/)  
> URL: https://www.haoyep.com/posts/ptatm-1/  


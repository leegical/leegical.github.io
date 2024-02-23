# 通过ZeroTier SSH连接内网主机

一些内网的主机可以访问公网，但是关闭了公网SSH端口。可以通过ZeroTier搭建VPC，让内网主机与client位于同一虚拟局域网中，实现SSH连接。
&lt;!--more--&gt;

zerotier官网：[https://www.zerotier.com/](https://www.zerotier.com/)

官方文档：[https://zerotier.atlassian.net/wiki/spaces/SD/overview](https://zerotier.atlassian.net/wiki/spaces/SD/overview)

## 目的
假设存在网络拓扑如下图：
![image](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311082253538.png)

内网中的主机A有公网访问权限，可以和PC通信。但是由于主机A没有公网IP或`ssh`等服务端口不向外网开放（主机A的服务端口只向内网机器开放），导致PC无法使用ssh等工具直接访问主机A。
我们要做的就是通过`ZeroTier`给PC、主机A创建一个`overlay`内网，忽略`underlay`，让PC、主机A以为双方都在同一个局域网内。这样PC就可以用`ZeroTier`内网IP来直接访问主机A了。

## 创建一个网络
### 创建网络
进入[zerotier官网](https://www.zerotier.com/)，用邮箱注册一个账号。然后进入[网络列表](https://my.zerotier.com/network)，点击Create A Network按钮创建一个网络.
![image](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311082253204.png)

下方列表中会出现一个网络ID，点击网络ID进入即可这个网络的设置界面。
![image](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311082253074.png)
记住这个网络ID，如图中为`a09acf0233953bab`

### 设置网络
1. `setting`
![image](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311082254838.png)

2. 设置网段
这里随便选一个，也可以保持默认。
如下图中，内网网段为`172.22.0.0/16`
![image](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311082254823.png)

## 加入网络
### 安装ZeroTier软件
安卓平台建议使用：[ZerotierFix](https://github.com/kaaass/ZerotierFix/releases)
其他平台直接从[官网下载](https://www.zerotier.com/download/)
### Windows
右键点击`ZeroTier`托盘图标——`Join New Networdk`——输入2.1中你获取的网络ID。本文中是`a09acf0233953bab`。点击`Join`加入网络。
![image](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311082254402.png)

回到网络设置网页，可以看到`Members`多了一个成员。
**勾选权限**，设置一个名字，便于区分。
![image](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311082255319.png)

### Linux——Ubuntu
#### 安装
输入以下命令在ubuntu中安装zerotier：
```bash
curl -s https://install.zerotier.com | sudo bash

## 设置开机自启
sudo systemctl enable zerotier-one
## 启动服务
sudo systemctl start zerotier-one
```

卸载命令：
```bash
sudo dpkg -P zerotier-one
sudo rm -rf /var/lib/zerotier-one/
```

#### 加入网络
运行以下命令并将`&lt;NETWORK-ID&gt;`替换为网络ID：
```bash
sudo zerotier-cli join &lt;NETWORK-ID&gt;
```
本文中即为：
```bash
sudo zerotier-cli join a09acf0233953bab
```
如果连接成功，应打印`200 join OK`输出。

同理，回到网络设置网页，可以看到`Members`多了一个成员。**权限打勾**，设置一个名字，便于区分。
记录下主机A的内网IP。本文中为`172.22.0.214`。
![image](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311082255710.png)

## 远程连接
### 确认网络权限
当你把所有设备都连接到网络中，记得将网络访问权限设置为`Private`，以增强安全性。
![image](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311082255006.png)

### 远程连接
以Windows连接Ubuntu为例，双方都已启动`ZeroTier`并加入同一个网络。
直接ssh主机A的内网IP即可：
![image](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311082255095.png)

---

> 作者: [云吱](https://haoyep.com/)  
> URL: https://haoyep.com/posts/zerotier-ssh/  


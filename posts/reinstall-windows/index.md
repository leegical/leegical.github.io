# 重装Windows系统记录


本文主要是记录给小白（女朋友）重装系统的流程，包括重装系统使用的工具和进入新系统后的软件配置。

<!--more-->

# 一、重装系统
## 1.1 启动盘工具
[ventoy](https://www.ventoy.net/cn/index.html)可以满足一个U盘安装多个系统，[下载地址](https://www.ventoy.net/cn/download.html)
![ventoy](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202301281546842.png)

插入U盘，打开`Ventoy2Disk.exe`，配置选项——分区类型，勾选`GPT`。
点击安装，**注意此步骤会清空U盘全部数据**。如果U盘已经安装过ventoy，则点击升级，升级操作不会清空U盘数据。

## 1.2 系统镜像文件
### Windows
建议直接[参考教程](https://zhuanlan.zhihu.com/p/370231492)从微软官网下载，[Windows11](https://www.microsoft.com/software-download/windows11)同理。原理是更改浏览器为非Windows UA以获取下载直链。注意，下载`Windows 10/11 64bit`版本，不要下载家庭中文版。

**注意事项**
- 建议选择**专业工作站**版本
- 条件允许的情况下，可以将Windows安装到200GB以上的分区（需提前清空该分区所有数据）。毕竟小白不懂，只会狂点下一步把软件都安装到C盘。
- Windows无法安装到这个磁盘，选中的磁盘采用GPT分区形式
>弹出这个提示，主要是电脑硬盘格式为GPT分区表，而U盘启动引导方式为“Legacy”模式，导致了开机引导方式和磁盘数据结构不匹配导致的问题！正确的开机引导方式和磁盘数据结构：Legacy引导对应的是MBR分区；UEFI引导对应的是GPT分区。
**推荐的解决方法：将U盘启动UEFI模式**
将电脑重启，重新选择U盘启动模式，在BIOS界面选择“UEFI：”开头的U盘名称。
同理，如果电脑硬盘格式为MBR，那么在BIOS界面选择不带“UEFI：”开头的U盘启动。
- 安装系统时建议使用本地账号登陆，账号名设为全英文。进入系统后再去设置里登录自己的微软账号
### Ubuntu 22.04 LTS
- [官网](https://releases.ubuntu.com/jammy/)
- [南京大学镜像](https://mirror.nju.edu.cn/ubuntu-releases/jammy/)
- [清华大学镜像](https://mirrors.tuna.tsinghua.edu.cn/ubuntu-releases/jammy/)
- [北邮镜像](https://mirrors.bupt.edu.cn/ubuntu-releases/jammy/)

### Ubuntu 20.04 LTS
- [官网](https://releases.ubuntu.com/focal/)
- [南京大学镜像](https://mirror.nju.edu.cn/ubuntu-releases/focal/)
- [清华大学镜像](https://mirrors.tuna.tsinghua.edu.cn/ubuntu-releases/focal/)
- [北邮镜像](https://mirrors.bupt.edu.cn/ubuntu-releases/focal/)

**注意事项**
Ubuntu分区没必要那么复杂，完全可以直接all in在一个硬盘分区上。总之，按需调整各逻辑分区对应的硬盘分区位置、大小。

# 二、Windows 软件设置
当给其他人安装软件时，切记以人为本，放下技术优越性，不要搞一些好用但需要折腾、破解的软件。小白需要的是稳定易维护，版本升级简单。
下面提到的软件都以易更新为主（微软商店、联想软件管家），部分特殊软件也保证可以锁死版本使用。
## 2.1 系统相关
- 系统激活：淘宝买激活码或者使用[HEU KMS Activator](https://www.ghxi.com/heukmsactivator.html)，可能会报毒，关闭Windows安全保护后再运行，或安装火绒后再运行。`用完即删`
- 驱动：[驱动天使](https://lestore.lenovo.com/detail/1120)、[驱动总裁](https://www.sysceo.com/Software-softwarei-id-264.html)  `用完即卸载`
- 软件卸载工具：[geek](https://geekuninstaller.com/)：单文件、免费、可以自动删除注册表等痕迹
- 微软常用运行库合集（[果核版本](https://ghpym.lanzoui.com/b00ze15ab#y9x2)）。`用完即删`
- DirectX修复工具（[果核版本](https://www.ghxi.com/directxfix.html)），启用扩展，强力修复C++。`用完即删`
- 多软件音量调节：[EarTrumpet](https://www.microsoft.com/store/productId/9NBLGGH516XP)
- 剪贴板增强：[Ditto Clipboard](https://www.microsoft.com/store/productId/9NBLGGH3ZBJQ)
- 多显示器亮度调节工具：[Twinkle Tray](https://www.microsoft.com/store/productId/9PLJWWSV01LK)
- 系统安全：[火绒](https://www.huorong.cn/person5.html)，下载完整版，开启广告拦截。安静无打扰
>也可以直接下载联想电脑管家，相当于集成了火绒、驱动管理、软件商店，还是很不错的。
## 2.2 办公类
- Office：[Office Tool Plus](https://otp.landian.vip/zh-cn/download.html) 选择包含框架的版本。`用完即删`
>产品Microsoft365 64位，选择Word、Excel、PowerPoint，如有需求可选安装OneNote、Visio等。先清除所有许可证，再安装激活`Office Mondo 2016 - 批量版`许可证。kms地址网上随便搜索填一个，如`kms.loli.beer`、`kms.03k.org`，端口不用填。
- PDF：[Adobe Acrobat DC  @vposy](https://www.aliyundrive.com/s/Btrj6BhFUjg)
- 思维导图：[百度脑图桌面离线版](https://ghproxy.com/https://github.com/NaoTu/DesktopNaotu/releases/download/v3.2.3/DesktopNaotu-win32-x64.zip)、可能需要科学上网[drawio](https://github.com/jgraph/drawio-desktop/releases)、支持正版[xmind](https://xmind.cn/)

## 2.3 工具类
- 软件商店：[联想应用商店](https://lestore.lenovo.com/about)
- 解压缩：NanaZip（[微软商店](https://apps.microsoft.com/store/detail/9N8G7TSCL18R?hl=zh-cn&gl=CN&rtc=1)）
- 图片：[2345看图王 果核版](https://www.123pan.com/s/HQeA-w21Sh#3519)，第一次使用，请使用绿化卸载.exe进行绿化
- 输入法：[搜狗输入法](https://shurufa.sogou.com/) 云联想、细胞词库仍然是天花板级别，广告就交给火绒拦截吧
- 截图：[Snipaste](https://www.microsoft.com/store/productId/9P1WXPKB68KX)
- 浏览器：edge（关闭后台运行、硬件加速）登录微软账号同步扩展、密码，或[Firefox](https://www.mozilla.org/zh-CN/firefox/)、[360极速浏览器X](https://browser.360.cn/eex/)
>不建议安装Chrome，除非会科学上网同步数据
>浏览器扩展推荐：[uBlock Origin 去广告](https://microsoftedge.microsoft.com/addons/detail/ublock-origin/odfafepnkmbhccpbejgmiehpchacaeak)、[Awesome Screenshot 截图录屏](https://microsoftedge.microsoft.com/addons/detail/awesome-screenshot-%E6%88%AA%E5%9B%BE%E5%BD%95%E5%B1%8F/gpmljinohlbfgmeoaeceoajachkabijo)、[Infinity 新标签页 (Pro)](https://microsoftedge.microsoft.com/addons/detail/infinity-%E6%96%B0%E6%A0%87%E7%AD%BE%E9%A1%B5-pro/hajlmbnnniemimmaehcefkamdadpjlfa)、[沙拉查词](https://microsoftedge.microsoft.com/addons/detail/%E6%B2%99%E6%8B%89%E6%9F%A5%E8%AF%8D%E8%81%9A%E5%90%88%E8%AF%8D%E5%85%B8%E5%88%92%E8%AF%8D%E7%BF%BB%E8%AF%91/idghocbbahafpfhjnfhpbfbmpegphmmp)、[学术需求：easyScholar](https://microsoftedge.microsoft.com/addons/detail/easyscholar/bpepicgagmdchlkjjeeiekpoafehpagm)
- 通讯：微信、QQ。不得不用，在联想应用商店里直接下载
- 桌面管理：[腾讯桌面管理](https://guanjia.qq.com/product/zmzl/)：去除快捷方式小箭头、替代everthing、关闭壁纸
![腾讯桌面管理](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202301290029000.png)

## 2.4 音视频（可选安装）
- 音乐
	- [洛雪音乐](https://lxmusic.toside.cn/download)，配合[六音音源](https://www.sixyin.com/download?post=8498)
	- [Listen 1](https://listen1.github.io/listen1/)，全平台免费听歌
- 本地音乐播放器：[MusicPlayer2](https://github.com/zhongyang219/MusicPlayer2/releases)
- 播放器：[potplayer](https://lestore.lenovo.com/detail/15654?origin=pcstore_copylink)
>Potplayer无边框设置：
>选项——基本——默认皮肤，勾选`视频下自动隐藏`、`全屏时防止遮盖`；进阶皮肤，方式设置为`使用 Direct3D 9`
![Potplayer无边框设置](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202301290159701.png)

## 2.5 下载工具（可选安装）
IDM+迅雷组合秒杀一切。下方都是特殊版本，没事别升级
- [IDM](https://www.423down.com/575.html)：有浏览器扩展，资源嗅探能力最强，下载速度也是最快。但没法下种子
- [NDM](https://www.neatdownloadmanager.com/index.php/en/)：IDM平替，免费，没汉化
- [Motrix](https://motrix.app/zh-CN/)：颜值高，能下种子。但有时会没速度


---

> 作者: [Leehow](https://www.haoyep.com/)  
> URL: https://www.haoyep.com/posts/reinstall-windows/  


# 利用 Cloudflare Pages 和 BPB 面板搭建免费VPN订阅节点


无需域名，无需 SSL，通过 Cloudflare 和 BPB Panel，搭建一个永久免费且高速的免费 VPN。结合 Cloudflare 实现优选订阅、永久免费 vless 节点订阅，为使用（singbox-core 和 xray-core）的跨平台客户端提供配置。

&lt;!--more--&gt;

## 前提
有一个 Cloudflare 账号，以及一个域名。
登录 [Cloudflare](https://dash.cloudflare.com/login?lang=zh-cn)。

## 创建 Pages
### 下载代码文件
从以下几个链接任选其一，下载最新的 `worker.zip` 到本地。
- [Github Release](https://github.com/bia-pain-bache/BPB-Worker-Panel/releases/latest/download/worker.zip)
- [中国大陆加速1](https://github.moeyy.xyz/https://github.com/bia-pain-bache/BPB-Worker-Panel/releases/latest/download/worker.zip)
- [中国大陆加速2](https://gh.xmly.dev/https://github.com/bia-pain-bache/BPB-Worker-Panel/releases/latest/download/worker.zip)
- [中国大陆加速3](https://gh.api.99988866.xyz/https://github.com/bia-pain-bache/BPB-Worker-Panel/releases/latest/download/worker.zip)

### 上传并创建
点击左侧栏 **Compute (Workers)** -&gt; 【Workers 和 Pages】，点击**创建**。
![创建 Pages](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202408282337943.png)

点击 **Pages** -&gt; 【上传资产】。
![上传worker](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202408290003016.png)

- 项目名称：随便取，但是不能包含 `bpb`。
- 上传压缩包：将第一步中下载的 `worker.zip` 上传。
![上传worker](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202408282356133.png)

稍等片刻，部署成功！
![部署成功](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202408290035625.png)

### 设置变量
部署成功后，点击右下角 **继续处理项目** 回到创建的 Pages 的界面。
点击 **设置** -&gt; 【变量和机密】，点击**添加**。添加以下3个变量：
- **UUID**：直接安装的 BPB 面板默认使用同一个 UUID [89b3cbba-e6ac-485a-9481-976a0415eab9]，可能存在安全隐患。可以去[在线生成 UUID 1](https://1024tools.com/uuid)  | [在线生成 UUID 2](https://www.lddgo.net/string/uuid) 等网站随机生成一个新的 UUID。
- **PROXYIP**：去这里[随机选择一个代理 IP](https://www.nslookup.io/domains/cdn.xn--b6gac.eu.org/dns-records/)，或者你也可以直接把代理 IP 设置为 `cdn-b100.xn--b6gac.eu.org` 或 `bpb.yousef.isegaro.com`。
- **TR_PASS**: 去[随机字符串生成器](https://www.jyshare.com/front-end/9111/) | [随机字符串生成](http://tool.pfan.cn/random) 生成一串复杂字符串做为密码。

![设置变量](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202408290005721.png)
## 绑定 KV
### 创建
点击左侧栏 **存储和数据库** -&gt; 【KV】，点击**创建**。
- 名称：随便取一个，但是不能包含 `bpb`。
![创建kv](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202408210057059.png)
### 绑定
回到创建的 Pages 界面。点击 **设置** -&gt; 【绑定】，点击**添加**，选择添加 KV 命名空间。
![添加KV](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202408290013516.png)
- 变量名称：能且仅能填写 `kv`
- KV 命名空间：选择[创建 KV](#创建-kv) 中设置的命名空间

![绑定kv](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202408290039050.png)

## 绑定域名（可选）
Cloudflare 为 Pages 分配的 `.pages.dev` 域名被墙了，无法直接访问。你可以为创建的 pages 设定一个自定义域名，从而访问它。

点击**自定义域**。假设你的域名是 `example.com`，这里分配一个三级域名 `shop.example.com` 给这个 page。这样，你就可以通过`shop.example.com/panel` 来访问你的面板了！
![设置自定义域名](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/20250112023744473.png)
## 重新部署
[设置变量](#设置变量)、[KV 空间绑定](#绑定)后，点击右上角 **创建部署**，再上传一次 `worker.zip`，重新部署。

&gt; [!NOTE]
&gt; 注意：在项目有任何改动后，都需要进行重新部署，否则改动不会生效。

![重新部署](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202408290046970.png)

## BPB 面板
访问项目网址： *https://你的项目地址.pages.dev/panel* 

或者 *https://自定义域名/panel* 。
### 修改密码
第一次访问面板会提示你修改密码，建议修改成一个复杂密码，避免面板被盗用。
![修改密码](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202408290050290.png)

### 面板配置
使用修改后的密码重新登录面板。
1) **FakeDNS**：可以设置为 enable，理论上会加快速度。但可能出现与浏览器 dns 缓存冲突等问题，导致无法正常上网。
2) **Proxy IPs / Domains**：填写`cdn-b100.xn--b6gac.eu.org`或`bpb.yousef.isegaro.com`
3) **Clean IPs / Domains**：前往 [Scan Now](https://scanner.github1.cloud/) 点击扫描 Clean IP。一般来说，Clean IP 的节点 RTT 会更短。

&gt; [!NOTE]
&gt; 为了扫描出与你实际网络通信时间最短的 IP，扫描时记得关闭代理。

点击 Start Scan，开始扫描。第一次扫描的 IP 数较少，你可以点击下方提示，扫描更多 IP。
![扫描Clean IP](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202408290102440.png)

将扫描到的 Clean IP 填到 BPB 面板配置中。
![Scan Now](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202408290057500.png)

4) TLS 端口处勾选你想启用的端口，或者默认使用443端口。
![启用TLS端口](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202408290056530.png)

5) **ROUTING RULES**：配置一些路由规则。**Bypass xxx**是指 xxx 不走代理（直连访问）；**Block xxx**是指 xxx 被屏蔽访问（无法访问）。可以按需勾选。
	- **Bypass LAN**：绕过本地局域网
	- **Block Ads**：屏蔽广告网址
	- **Bypass Iran**：绕过伊朗
	- **Block Porn**：屏蔽颜色网站
	- **Bypass China**：绕过中国大陆
	- **Block QUIC**：屏蔽 QUIC 协议
	- **Bypass Russia**：绕过俄罗斯
	- **CUSTOM RULES**：除了上面预设的规则外，你可以在这里自定义一些需要直连（Bypass）和屏蔽（Block）的 IP 地址/网站。
	![路由规则](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202408290053190.png)

最后，点击 **APPLY SETTINGS**，应用设置。
### 导入节点
根据你所使用的代理应用，点击对应的 **COPY SUB** 按钮，复制 BPB 面板生成的订阅链接。

![复制订阅链接](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202408290110711.png)

#### PC-V2rayN
##### 导入
打开 V2rayN，【订阅分组】-&gt;【订阅分组设置】-&gt;【添加】
- 别名：随机写一个
- 可选地址：输入 BPB 面板导出的订阅链接
![V2rayN导入订阅链接](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202408290114711.png)

##### 更新/获取节点
【订阅分组】-&gt;【更新全部订阅(不通过代理)】，获取节点
![获取节点](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202408290117981.png)

#### 安卓-V2rayNG
##### 导入
【左上角三条横线】-&gt;【订阅分组设置】-&gt; 右上角`&#43;`
![新建订阅分组](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202408290125388.png)

- 备注：随便写一个
- 可选地址：输入 BPB 面板导出的订阅链接
![添加订阅分组](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202408290127693.png)

##### 更新/获取节点
首页右上角三个点 -&gt; 更新订阅
![更新订阅](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202408290131358.png)

### 修改密码
如果你觉得原来设置的密码太简单，也可以重新修改密码。
登录你的 BPB 面板，到页面最底端，点击 **Change Password** 来修改密码。
![修改密码](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202408290120104.png)


---

> 作者: [Leehow](https://www.haoyep.com/)  
> URL: https://www.haoyep.com/posts/cf-bpb-vpn/  


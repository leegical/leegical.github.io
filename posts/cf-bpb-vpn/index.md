# 利用 Cloudflare Pages 和 BPB 面板搭建个人专属免费VPN订阅节点, 避免 1101 等报错


无需域名，无需 SSL，通过 Cloudflare 和 BPB Panel，解决1101等报错，搭建一个个人专属永久免费且高速的免费 VPN。结合 Cloudflare 实现优选订阅永久免费节点订阅，为使用（singbox-core 和 xray-core）的跨平台客户端提供配置。

&lt;!--more--&gt;

## 搭建思路
当前 Cloudflare 收紧了 BPB 等项目的审查，直接使用源码或者原作者提供的混淆代码，很容易出现1101的报错。合理推测 Cloudflare 通过以下方面做了限制：
- 代理类关键词：如 `vless`
- 项目类关键词：如 `bpb`
- 源码：如某个代理类代码被多次使用（这也是为什么混淆代码刚开始好使，过两三天又会出现1101的原因）

混淆代码可以绕过 Cloudflare 的审查，前提是使用同一份混淆代码的人不多。BPB 项目现在也提供了未混淆加密前的[源代码](https://github.com/bia-pain-bache/BPB-Worker-Panel/blob/main/unobfuscated/worker.js)，我们可以加密该代码来获得自己独一无二的混淆代码，从而成功完成搭建。

&gt; [!NOTE]
&gt; 如果你已经有成功搭建且运行很长时间的 BPB，不要轻易更新 `_worker.js`！能用就不要动！如果想体验新版本 BPB，可以重新创建个 worker。
## 前提
- Github 账号：通过 Github action 自动拉取最新源代码并进行混淆
- Cloudflare 账号
- 域名：解决 Cloudflare Pages 自带域名被墙

## 混淆代码
新建一个 Github 仓库，在仓库里新建文件夹 `.github/workflows`，并在该文件夹中创建 `Obfuscate.yml` 文件，粘贴代码如下（也可以去我提供的 [demoPanel示例仓库](https://github.com/leegical/demoPanel/) 中复制相关代码。）：
```yml
name: Build Obfuscate BPB Panel

on:
  push:
    branches:
      - main
  schedule:
        # Runs everyday at 1:00 AM
        - cron: &#34;0 1 * * *&#34;

permissions:
  contents: write

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Check out the code
        uses: actions/checkout@v4

      - name: Set up Node.js
        uses: actions/setup-node@v4
        with:
          node-version: &#34;latest&#34;

      - name: Install dependencies
        run: |
          npm install -g javascript-obfuscator

      - name: Clone BPB workjs
        run: |
          wget -O origin.js https://raw.githubusercontent.com/bia-pain-bache/BPB-Worker-Panel/refs/heads/main/unobfuscated/worker.js
      
      - name: Obfuscate BPB worker js
        run: |
          javascript-obfuscator origin.js --output _worker.js \
          --compact true \
          --control-flow-flattening true \
          --control-flow-flattening-threshold 1 \
          --dead-code-injection true \
          --dead-code-injection-threshold 1 \
          --identifier-names-generator hexadecimal \
          --rename-globals true \
          --string-array true \
          --string-array-encoding &#39;rc4&#39; \
          --string-array-threshold 1 \
          --transform-object-keys true \
          --unicode-escape-sequence true

      - name: Commit changes
        uses: stefanzweifel/git-auto-commit-action@v5
        with:
          branch: main
          commit_message: &#39;:arrow_up: update latest bpb panel&#39;
          commit_author: &#39;github-actions[bot] &lt;github-actions[bot]@users.noreply.github.com&gt;&#39;
          push_options: &#39;--set-upstream&#39;
```

&gt; [!NOTE]
&gt; 仓库主分支名需为 **main**。

`Obfuscate.yml` 为你的代码仓库创建了一个 action，它将在每次 main 分支有 push 时、每天1点钟下载最新的 BPB 源代码，并执行混淆。

push `Obfuscate.yml` 到你的代码仓库。稍等片刻，仓库根目录中会出现两个新的文件：
- `origin.js`：最新未加密的 BPB 源代码 
- `_worker.js`：混淆后的个人专属 BPB 代码
![自动构建的文件](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/20250120234002592.png)

下载混淆后的代码文件 `_worker.js` 到本地，压缩为 `worker.zip`.

## 创建 Pages
登录 [Cloudflare](https://dash.cloudflare.com/login?lang=zh-cn)。
### 上传并创建
点击左侧栏 **Compute (Workers)** -&gt; 【Workers 和 Pages】，点击**创建**。
![创建 Pages](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202408282337943.png)

点击 **Pages** -&gt; 【上传资产】。
![上传worker](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202408290003016.png)

- 项目名称：随便取，但是不能包含 `bpb`。
- 上传压缩包：将通过混淆代码创建的 `worker.zip` 上传。
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
打开面板网址： *https://你的项目地址.pages.dev/panel* 

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


# Windows下使用hugo和Github Pages配置博客


本文介绍了如何使用 hugo 和 Github Pages 免费搭建个人博客，并使用自定义域名访问。

&lt;!--more--&gt;

## 前提
默认本地已安装了 [Git](https://git-scm.com/downloads)、[VSCode](https://code.visualstudio.com/Download)。
## hugo 配置
### [安装 Hugo](https://gohugo.io/installation/windows/)
推荐使用 `Hugo extended` 版本
#### 预构建的二进制文件
访问[最新版本](https://github.com/gohugoio/hugo/releases/latest)页面，然后向下滚动到**Assets**部分。选择对应平台下载。
![hugo发布页面](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311081636173.png)

解压到某个目录，然后将该目录添加到环境变量中：
![添加hugo到环境变量](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311081636306.png)

#### 通过包管理器（Windows）
##### [Chocolatey](https://gohugo.io/installation/windows/#chocolatey)
[Chocolatey](https://chocolatey.org/) 是一个免费的开源 Windows 包管理器。这将安装 Hugo 的扩展版本：
```sh
choco install hugo-extended
```
##### [Scoop](https://gohugo.io/installation/windows/#scoop)
[Scoop](https://scoop.sh/) 是适用于 Windows 的免费开源包管理器。这将安装 Hugo 的扩展版本：
```sh
scoop install hugo-extended
```
##### [Winget](https://gohugo.io/installation/windows/#winget)
[Winget](https://learn.microsoft.com/en-us/windows/package-manager/) 是 Microsoft 的官方免费开源 Windows 包管理器。这将安装 Hugo 的扩展版本：
```sh
winget install Hugo.Hugo.Extended
```
### 创建 Hugo 网站
通过上述操作安装 hugo 程序后，就可以通过 `hugo new site` 命令进行网站创建、配置与本地调试了。
选择一个本地文件夹作为根目录，右键——`Git Bash Here`，输入下面的命令
```bash
hugo new site &lt;site-name&gt;
```
![hugo new site 命令进行网站创建](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311081636474.png)

**注：后续命令未经说明，均在 Git Bash 中的 `E:\Workspace\blog` 目录下运行**
### 主题
#### 安装
推荐使用 [**FixIt** 主题](https://github.com/hugo-fixit/FixIt)。
初始化你的项目目录为一个空的 Git 存储库，将 [FixIt][fixit] 主题克隆到 `themes` 目录中，将其作为 [Git 子模块][git-submodule] 添加到您的项目中。

```bash
git init
git submodule add https://github.com/hugo-fixit/FixIt.git themes/FixIt
```

如果你想使用 `dev` 分支上的版本，可以使用以下命令：

```bash
git submodule add -b dev https://github.com/hugo-fixit/FixIt.git themes/FixIt
```

或者将子模块分支从 `master` 切换到 `dev`：

```bash
git submodule set-branch -b dev themes/FixIt
```
#### 基础配置
用`VScode`打开`E:\Workspace\blog`文件夹，用下面的内容覆盖`hugo.toml`文件。并自行修改`baseURL`和`title`。
其中，`baseURL`为`你的github账户名.github.io`，也可以像我一样设置自定义域名。记得逐项修改为你的配置。
```toml
# =====================================================================================
# It&#39;s recommended to use Alternate Theme Config to configure FixIt
# Modifying this file may result in merge conflict
# =====================================================================================

# -------------------------------------------------------------------------------------
# Hugo Configuration
# See: https://gohugo.io/getting-started/configuration/
# -------------------------------------------------------------------------------------

# 网站标题
title = &#34;Leehow的小站&#34;
# Hostname (and path) to the root
baseURL = &#34;https://www.haoyep.com/&#34;
# baseURL = &#34;https://leegical.github.io/&#34;
# 更改使用 Hugo 构建网站时使用的默认主题
theme = [&#34;FixIt&#34;]
# determines default content language [&#34;en&#34;, &#34;zh-cn&#34;, &#34;fr&#34;, &#34;pl&#34;, ...]
defaultContentLanguage = &#34;zh-cn&#34;
# 网站语言, 仅在这里 CN 大写 [&#34;en&#34;, &#34;zh-CN&#34;, &#34;fr&#34;, &#34;pl&#34;, ...]
languageCode = &#34;zh-CN&#34;
# 语言名称 [&#34;English&#34;, &#34;简体中文&#34;, &#34;Français&#34;, &#34;Polski&#34;, ...]
languageName = &#34;简体中文&#34;
# 是否包括中日韩文字
hasCJKLanguage = true
# default amount of posts in each pages
paginate = 12
# copyright description used only for seo schema
copyright = &#34;&#34;
# whether to use robots.txt
enableRobotsTXT = true
# whether to use git commit log
enableGitInfo = true
# whether to use emoji code
enableEmoji = true

# -------------------------------------------------------------------------------------
# Menu Configuration
# See: https://fixit.lruihao.cn/documentation/basics/#menu-configuration
# -------------------------------------------------------------------------------------

[menu]
  [[menu.main]]
    identifier = &#34;posts&#34;
    # you can add extra information before the name (HTML format is supported), such as icons
    pre = &#34;&#34;
    # you can add extra information after the name (HTML format is supported), such as icons
    post = &#34;&#34;
    name = &#34;文章&#34;
    url = &#34;/posts/&#34;
    # title will be shown when you hover on this menu link
    title = &#34;&#34;
    weight = 1
    # FixIt 0.2.14 | NEW add user-defined content to menu items
    [menu.main.params]
      # add css class to a specific menu item
      class = &#34;&#34;
      # whether set as a draft menu item whose function is similar to a draft post/page
      draft = false
      # FixIt 0.2.16 | NEW add fontawesome icon to a specific menu item
      icon = &#34;fa-solid fa-archive&#34;
      # FixIt 0.2.16 | NEW set menu item type, optional values: [&#34;mobile&#34;, &#34;desktop&#34;]
      type = &#34;&#34;
  [[menu.main]]
    identifier = &#34;categories&#34;
    pre = &#34;&#34;
    post = &#34;&#34;
    name = &#34;分类&#34;
    url = &#34;/categories/&#34;
    title = &#34;&#34;
    weight = 2
    [menu.main.params]
      icon = &#34;fa-solid fa-th&#34;
  [[menu.main]]
    identifier = &#34;tags&#34;
    pre = &#34;&#34;
    post = &#34;&#34;
    name = &#34;标签&#34;
    url = &#34;/tags/&#34;
    title = &#34;&#34;
    weight = 3
    [menu.main.params]
      icon = &#34;fa-solid fa-tags&#34;

# -------------------------------------------------------------------------------------
# Theme Core Configuration
# See: https://fixit.lruihao.cn/documentation/basics/#theme-configuration
# -------------------------------------------------------------------------------------

[params]
  # FixIt 0.2.15 | CHANGED FixIt theme version
  version = &#34;0.2.X&#34; # e.g. &#34;0.2.X&#34;, &#34;0.2.15&#34;, &#34;v0.2.15&#34; etc.
  # 网站描述
  description = &#34;&#34;
  # 网站关键词
  keywords = [&#34;程序员&#34;]
  # 网站默认主题样式 [&#34;light&#34;, &#34;dark&#34;, &#34;auto&#34;]
  defaultTheme = &#34;auto&#34;
  # 公共 git 仓库路径，仅在 enableGitInfo 设为 true 时有效
  gitRepo = &#34;&#34;
  #  哪种哈希函数用来 SRI, 为空时表示不使用 SRI
  # [&#34;sha256&#34;, &#34;sha384&#34;, &#34;sha512&#34;, &#34;md5&#34;]
  fingerprint = &#34;sha256&#34;
  #  日期格式
  dateFormat = &#34;2006-01-02&#34;
  # 网站图片，用于 Open Graph 和 Twitter Cards
  images = [&#34;/logo.png&#34;]
  #  开启 PWA 支持
  enablePWA = true
  #  是否自动显示外链图标
  externalIcon = false
  #  默认情况下，FixIt 只会在主页的 HTML 头中注入主题元标记
  # 您可以将其关闭，但如果您不这样做，我们将不胜感激，因为这是观察 FixIt 受欢迎程度上升的好方法
  disableThemeInject = false

  # 作者配置
  [params.author]
    name = &#34;&#34;
    email = &#34;&#34;
    link = &#34;&#34;
    avatar = &#34;&#34;

  # 应用图标配置
  [params.app]
    # 当添加到 iOS 主屏幕或者 Android 启动器时的标题，覆盖默认标题
    title = &#34;Leehow的小站&#34;
    # 是否隐藏网站图标资源链接
    noFavicon = false
    # 更现代的 SVG 网站图标，可替代旧的 .png 和 .ico 文件
    svgFavicon = &#34;/favicon.svg&#34;
    # Safari 图标颜色
    iconColor = &#34;#5bbad5&#34;
    # Windows v8-10 磁贴颜色
    tileColor = &#34;#da532c&#34;
    #  Android 浏览器主题色
    [params.app.themeColor]
      light = &#34;#f8f8f8&#34;
      dark = &#34;#252627&#34;

  # 搜索配置
  [params.search]
    enable = true
    # 搜索引擎的类型 [&#34;lunr&#34;, &#34;algolia&#34;, &#34;fuse&#34;]
    type = &#34;lunr&#34;
    # 文章内容最长索引长度
    contentLength = 4000
    # 搜索框的占位提示语
    placeholder = &#34;&#34;
    #  最大结果数目
    maxResultLength = 10
    #  结果内容片段长度
    snippetLength = 50
    #  搜索结果中高亮部分的 HTML 标签
    highlightTag = &#34;em&#34;
    #  是否在搜索索引中使用基于 baseURL 的绝对路径
    absoluteURL = false
    [params.search.algolia]
      index = &#34;&#34;
      appID = &#34;&#34;
      searchKey = &#34;&#34;
    [params.search.fuse]
      #  https://fusejs.io/api/options.html
      isCaseSensitive = false
      minMatchCharLength = 2
      findAllMatches = false
      location = 0
      threshold = 0.3
      distance = 100
      ignoreLocation = false
      useExtendedSearch = false
      ignoreFieldNorm = false

  # 页面头部导航栏配置
  [params.header]
    #  桌面端导航栏模式 [&#34;sticky&#34;, &#34;normal&#34;, &#34;auto&#34;]
    desktopMode = &#34;sticky&#34;
    #  移动端导航栏模式 [&#34;sticky&#34;, &#34;normal&#34;, &#34;auto&#34;]
    mobileMode = &#34;auto&#34;
    #  页面头部导航栏标题配置
    [params.header.title]
      # LOGO 的 URL
      logo = &#34;/logo.png&#34;
      # 标题名称
      name = &#34;Leehow的小站&#34;
      # 你可以在名称（允许 HTML 格式）之前添加其他信息，例如图标
      pre = &#34;&#34;
      # 你可以在名称（允许 HTML 格式）之后添加其他信息，例如图标
      post = &#34;&#34;
      #  是否为标题显示打字机动画
      typeit = false
    #  页面头部导航栏副标题配置
    [params.header.subtitle]
      # 副标题名称
      name = &#34;&#34;
      # 是否为副标题显示打字机动画
      typeit = false

  # FixIt 0.2.18 | NEW Breadcrumb config
  [params.breadcrumb]
    enable = false
    sticky = false
    showHome = false

  # 页面底部信息配置
  [params.footer]
    enable = true
    #  自定义内容（支持 HTML 格式）
    # 进阶使用，见参数 `params.customFilePath.footer`
    custom = &#34;&#34;
    #  是否显示 Hugo 和主题信息
    hugo = false
    #  是否显示版权信息
    copyright = true
    #  是否显示作者
    author = true
    # 网站创立年份
    since = 2019
    #  是否显示网站内容总字数
    wordCount = true
    #  公网安备信息，仅在中国使用（支持 HTML 格式）
    gov = &#34;&#34;
    #  ICP 备案信息，仅在中国使用（支持 HTML 格式）
    icp = &#34;&#34;
    # 许可协议信息（支持 HTML 格式）
    license = &#39;&lt;a rel=&#34;license external nofollow noopener noreferrer&#34; href=&#34;https://creativecommons.org/licenses/by-nc/4.0/&#34; target=&#34;_blank&#34;&gt;CC BY-NC 4.0&lt;/a&gt;&#39;
    #  网站创立时间
    [params.footer.siteTime]
      enable = true
      animate = true
      icon = &#34;fa-solid fa-heartbeat&#34;
      pre = &#34;&#34;
      value = &#34;2018-02-06T11:15:22&#43;08:00&#34; # e.g. &#34;2021-12-18T16:15:22&#43;08:00&#34;
    #  页面底部行排序，可选值：[&#34;first&#34;, 0, 1, 2, 3, 4, 5, &#34;last&#34;]
    [params.footer.order]
      powered = 0
      copyright = 0
      statistics = 0
      visitor = 0
      beian = 0

  #  Section（所有文章）页面配置
  [params.section]
    # section 页面每页显示文章数量
    paginate = 20
    # 日期格式（月和日）
    dateFormat = &#34;01-02&#34;
    # RSS 文章数目
    rss = 10
    #  最近更新文章设置
    [params.section.recentlyUpdated]
      enable = true
      rss = true
      days = 30
      maxCount = 10

  #  List（目录或标签）页面配置
  [params.list]
    # list 页面每页显示文章数量
    paginate = 20
    # 日期格式（月和日）
    dateFormat = &#34;01-02&#34;
    # RSS 文章数目
    rss = 10

  # 标签云配置
  [params.tagcloud]
    enable = false
    min = 14 # 最小字体大小，单位：px
    max = 32 # 最大字体大小，单位：px
    peakCount = 10 # 每个标签的最大文章数
    orderby = &#34;name&#34; # 标签排序方式，可选值：[&#34;name&#34;, &#34;count&#34;]

  # 主页配置
  [params.home]
    #  RSS 文章数目
    rss = 10
    # 主页个人信息
    [params.home.profile]
      enable = true
      # Gravatar 邮箱，用于优先在主页显示的头像
      gravatarEmail = &#34;&#34;
      # 主页显示头像的 URL
      avatarURL = &#34;/avatar.jpg&#34;
      #  头像菜单链接的 identifier
      avatarMenu = &#34;&#34;
      #  主页显示的网站标题（支持 HTML 格式）
      title = &#34;Leehow的小站&#34;
      # 主页显示的网站副标题
      subtitle = &#34;色相事一刹那，光阴里无尽藏&#34;
      # 是否为副标题显示打字机动画
      typeit = true
      # 是否显示社交账号
      social = true
      #  免责声明（支持 HTML 格式）
      disclaimer = &#34;&#34;
    # 主页文章列表
    [params.home.posts]
      enable = true
      # 主页每页显示文章数量
      paginate = 10

  # FixIt 0.2.16 | CHANGED Social config about the author
  [params.social]
    GitHub = &#34;&#34;
    Linkedin = &#34;&#34;
    Twitter = &#34;&#34;
    Instagram = &#34;&#34;
    Facebook = &#34;&#34;
    Telegram = &#34;&#34;
    Medium = &#34;&#34;
    Gitlab = &#34;&#34;
    Youtubelegacy = &#34;&#34;
    Youtubecustom = &#34;&#34;
    Youtubechannel = &#34;&#34;
    Tumblr = &#34;&#34;
    Quora = &#34;&#34;
    Keybase = &#34;&#34;
    Pinterest = &#34;&#34;
    Reddit = &#34;&#34;
    Codepen = &#34;&#34;
    FreeCodeCamp = &#34;&#34;
    Bitbucket = &#34;&#34;
    Stackoverflow = &#34;&#34;
    Weibo = &#34;&#34;
    Odnoklassniki = &#34;&#34;
    VK = &#34;&#34;
    Flickr = &#34;&#34;
    Xing = &#34;&#34;
    Snapchat = &#34;&#34;
    Soundcloud = &#34;&#34;
    Spotify = &#34;&#34;
    Bandcamp = &#34;&#34;
    Paypal = &#34;&#34;
    Fivehundredpx = &#34;&#34;
    Mix = &#34;&#34;
    Goodreads = &#34;&#34;
    Lastfm = &#34;&#34;
    Foursquare = &#34;&#34;
    Hackernews = &#34;&#34;
    Kickstarter = &#34;&#34;
    Patreon = &#34;&#34;
    Steam = &#34;&#34;
    Twitch = &#34;&#34;
    Strava = &#34;&#34;
    Skype = &#34;&#34;
    Whatsapp = &#34;&#34;
    Zhihu = &#34;&#34;
    Douban = &#34;&#34;
    Angellist = &#34;&#34;
    Slidershare = &#34;&#34;
    Jsfiddle = &#34;&#34;
    Deviantart = &#34;&#34;
    Behance = &#34;&#34;
    Dribbble = &#34;&#34;
    Wordpress = &#34;&#34;
    Vine = &#34;&#34;
    Googlescholar = &#34;&#34;
    Researchgate = &#34;&#34;
    Mastodon = &#34;&#34;
    Thingiverse = &#34;&#34;
    Devto = &#34;&#34;
    Gitea = &#34;&#34;
    XMPP = &#34;&#34;
    Matrix = &#34;&#34;
    Bilibili = &#34;&#34;
    ORCID = &#34;&#34;
    Liberapay = &#34;&#34;
    Ko-Fi = &#34;&#34;
    BuyMeaCoffee = &#34;&#34;
    Linktree = &#34;&#34;
    QQ = &#34;&#34;
    QQGroup = &#34;&#34; # https://qun.qq.com/join.html
    Diaspora = &#34;&#34;
    CSDN = &#34;&#34;
    Discord = &#34;&#34;
    DiscordInvite = &#34;&#34;
    Lichess = &#34;&#34;
    Pleroma = &#34;&#34;
    Kaggle = &#34;&#34;
    MediaWiki= &#34;&#34;
    Plume = &#34;&#34;
    HackTheBox = &#34;&#34;
    RootMe = &#34;&#34;
    Feishu = &#34;&#34;
    TryHackMe = &#34;&#34;
    Douyin = &#34;&#34;
    TikTok = &#34;&#34;
    Phone = &#34;&#34;
    Email = &#34;&#34;
    RSS = true

  #  文章页面配置
  [params.page]
    #  是否启用文章作者头像
    authorAvatar = true
    #  是否在主页隐藏一篇文章
    hiddenFromHomePage = false
    #  是否在搜索结果中隐藏一篇文章
    hiddenFromSearch = false
    #  是否使用 twemoji
    twemoji = false
    # 是否使用 lightgallery
    #  如果设为 &#34;force&#34;，文章中的图片将强制按照画廊形式呈现
    lightgallery = true
    #  是否使用 ruby 扩展语法
    ruby = true
    #  是否使用 fraction 扩展语法
    fraction = true
    #  是否使用 fontawesome 扩展语法
    fontawesome = true
    # 许可协议信息（支持 HTML 格式）
    license = &#39;&lt;a rel=&#34;license external nofollow noopener noreferrer&#34; href=&#34;https://creativecommons.org/licenses/by-nc/4.0/&#34; target=&#34;_blank&#34;&gt;CC BY-NC 4.0&lt;/a&gt;&#39;
    # 是否在文章页面显示原始 Markdown 文档链接
    linkToMarkdown = true
    #  是否在 RSS 中显示全文内容
    rssFullText = false
    #  页面样式 [&#34;narrow&#34;, &#34;normal&#34;, &#34;wide&#34;, ...]
    pageStyle = &#34;normal&#34;
    #   强制使用 Gravatar 作为作者头像
    # gravatarForce = true
    #  开启自动书签支持
    # 如果为 true，则在关闭页面时保存阅读进度
    autoBookmark = true
    #  是否使用 字数统计
    wordCount = true
    #  是否使用 预计阅读
    readingTime = true
    #  文章结束标志
    endFlag = &#34;&#34;
    #  是否开启即时页面
    instantPage = false
    # FixIt 0.3.0 | 是否在侧边栏开启合集
    collectionList = true
    # FixIt 0.3.0 | NEW whether to enable collection navigation at the end of the post
    collectionNavigation = false

    # FixIt 0.2.15 | 转载配置
    [params.page.repost]
      enable = false
      url = &#34;&#34;
    #  目录配置
    [params.page.toc]
      # 是否使用目录
      enable = true
      #  是否保持使用文章前面的静态目录
      keepStatic = false
      # 是否使侧边目录自动折叠展开
      auto = false
      #  目录位置 [&#34;left&#34;, &#34;right&#34;]
      position = &#34;right&#34;
    #  在文章开头显示提示信息，提醒读者文章内容可能过时
    [params.page.expirationReminder]
      enable = true
      # 如果文章最后更新于这天数之前，显示提醒
      reminder = 90
      # 如果文章最后更新于这天数之前，显示警告
      warning = 180
      # 如果文章到期是否关闭评论
      closeComment = false
    # FixIt 0.2.16 | 数学公式 CHANGED KaTeX mathematical formulas (https://katex.org)
    [params.page.math]
      enable = true
      # 默认行内定界符是 $ ... $ 和 \( ... \)
      inlineLeftDelimiter = &#34;&#34;
      inlineRightDelimiter = &#34;&#34;
      # 默认块定界符是 $$ ... $$, \[ ... \],  \begin{equation} ... \end{equation} 和一些其它的函数
      blockLeftDelimiter = &#34;&#34;
      blockRightDelimiter = &#34;&#34;
      # KaTeX 插件 copy_tex
      copyTex = true
      # KaTeX 插件 mhchem
      mhchem = true
    #  代码配置
    [params.page.code]
      # 是否显示代码块的复制按钮
      copy = true
      #  是否显示代码块的编辑按钮
      edit = true
      # 默认展开显示的代码行数
      maxShownLines = 10
    # FixIt 0.2.14 | 文章编辑
    [params.page.edit]
      enable = false
      # FixIt 0.2.15 | 编辑的基础链接
      # url = &#34;/edit/branch-name/subdirectory-name&#34; # base on `params.gitRepo`
      # url = &#34;https://github.com/user-name/repo-name/edit/branch-name/subdirectory-name&#34; # full url
      url = &#34;&#34;
    # FixIt 0.2.0 | Mapbox GL JS 配置 (https://docs.mapbox.com/mapbox-gl-js)
    [params.page.mapbox]
      # Mapbox GL JS 的 access token
      accessToken = &#34;&#34;
      # 浅色主题的地图样式
      lightStyle = &#34;mapbox://styles/mapbox/light-v9&#34;
      # 深色主题的地图样式
      darkStyle = &#34;mapbox://styles/mapbox/dark-v9&#34;
      # 是否添加 NavigationControl
      navigation = true
      # 是否添加 GeolocateControl
      geolocate = true
      # 是否添加 ScaleControl
      scale = true
      # 是否添加 FullscreenControl
      fullscreen = true
    # FixIt 0.2.17 | NEW 赞赏设置
    [params.page.reward]
      enable = false
      animation = false
      # 相对于页脚的位置，可选值：[&#34;before&#34;, &#34;after&#34;]
      position = &#34;after&#34;
      # comment = &#34;Buy me a coffee&#34;
      #  二维码图片展示模式，可选值：[&#34;static&#34;, &#34;fixed&#34;]，默认：`static`
      mode = &#34;static&#34;
      [params.page.reward.ways]
        # wechatpay = &#34;/images/wechatpay.png&#34;
        # alipay = &#34;/images/alipay.png&#34;
        # paypal = &#34;/images/paypal.png&#34;
        # bitcoin = &#34;/images/bitcoin.png&#34;
    #  文章页面的分享信息设置
    [params.page.share]
      enable = true
      Twitter = true
      Facebook = true
      Linkedin = false
      Whatsapp = true
      Pinterest = false
      Tumblr = false
      HackerNews = false
      Reddit = false
      VK = false
      Buffer = false
      Xing = false
      Line = true
      Instapaper = false
      Pocket = false
      Flipboard = false
      Weibo = true
      Myspace = true
      Blogger = true
      Baidu = false
      Odnoklassniki = false
      Evernote = true
      Skype = false
      Trello = false
      Mix = false
    # 评论系统设置
    [params.page.comment]
      enable = true
      # FixIt 0.2.13 | NEW Artalk comment config (https://artalk.js.org/)
      [params.page.comment.artalk]
        enable = false
        server = &#34;https://yourdomain&#34;
        site = &#34;默认站点&#34;
        placeholder = &#34;&#34;
        noComment = &#34;&#34;
        sendBtn = &#34;&#34;
        editorTravel = true
        flatMode = &#34;auto&#34;
        # FixIt 0.2.17 | CHANGED enable lightgallery support
        lightgallery = false
        locale = &#34;&#34; # FixIt 0.2.15 | NEW
        # FixIt 0.2.18 | NEW
        emoticons = &#34;&#34;
        nestMax = 2
        nestSort = &#34;DATE_ASC&#34; # [&#34;DATE_ASC&#34;, &#34;DATE_DESC&#34;, &#34;VOTE_UP_DESC&#34;]
        vote = true
        voteDown = false
        uaBadge = true
        listSort = true
        imgUpload = true
        preview = true
        versionCheck = true
      # FixIt 0.1.1 | NEW Disqus comment config (https://disqus.com)
      [params.page.comment.disqus]
        enable = false
        # Disqus shortname to use Disqus in posts
        shortname = &#34;&#34;
      # FixIt 0.1.1 | NEW Gitalk comment config (https://github.com/gitalk/gitalk)
      [params.page.comment.gitalk]
        enable = false
        owner = &#34;&#34;
        repo = &#34;&#34;
        clientId = &#34;&#34;
        clientSecret = &#34;&#34;
      # Valine comment config (https://github.com/xCss/Valine)
      [params.page.comment.valine]
        enable = false
        appId = &#34;&#34;
        appKey = &#34;&#34;
        placeholder = &#34;&#34;
        avatar = &#34;mp&#34;
        meta = &#34;&#34;
        requiredFields = &#34;&#34;
        pageSize = 10
        lang = &#34;&#34;
        visitor = true
        recordIP = true
        highlight = true
        enableQQ = false
        serverURLs = &#34;&#34;
        # FixIt 0.2.6 | NEW emoji data file name, default is &#34;google.yml&#34;
        # [&#34;apple.yml&#34;, &#34;google.yml&#34;, &#34;facebook.yml&#34;, &#34;twitter.yml&#34;]
        # located in &#34;themes/FixIt/assets/lib/valine/emoji/&#34; directory
        # you can store your own data files in the same path under your project:
        # &#34;assets/lib/valine/emoji/&#34;
        emoji = &#34;&#34;
        commentCount = true # FixIt 0.2.13 | NEW
      # FixIt 0.2.16 | CHANGED Waline comment config (https://waline.js.org)
      [params.page.comment.waline]
        enable = false
        serverURL = &#34;&#34;
        pageview = false # FixIt 0.2.15 | NEW
        emoji = [&#34;//unpkg.com/@waline/emojis@1.1.0/weibo&#34;]
        meta = [&#34;nick&#34;, &#34;mail&#34;, &#34;link&#34;]
        requiredMeta = []
        login = &#34;enable&#34;
        wordLimit = 0
        pageSize = 10
        imageUploader = false # FixIt 0.2.15 | NEW
        highlighter = false # FixIt 0.2.15 | NEW
        comment = false # FixIt 0.2.15 | NEW
        texRenderer = false # FixIt 0.2.16 | NEW
        search = false # FixIt 0.2.16 | NEW
        recaptchaV3Key = &#34;&#34; # FixIt 0.2.16 | NEW
        reaction = false # FixIt 0.2.18 | NEW
      # Facebook comment config (https://developers.facebook.com/docs/plugins/comments)
      [params.page.comment.facebook]
        enable = false
        width = &#34;100%&#34;
        numPosts = 10
        appId = &#34;&#34;
        languageCode = &#34;&#34;
      # FixIt 0.2.0 | NEW Telegram comments config (https://comments.app)
      [params.page.comment.telegram]
        enable = false
        siteID = &#34;&#34;
        limit = 5
        height = &#34;&#34;
        color = &#34;&#34;
        colorful = true
        dislikes = false
        outlined = false
      # FixIt 0.2.0 | NEW Commento comment config (https://commento.io)
      [params.page.comment.commento]
        enable = false
      # FixIt 0.2.5 | NEW Utterances comment config (https://utteranc.es)
      [params.page.comment.utterances]
        enable = false
        # owner/repo
        repo = &#34;&#34;
        issueTerm = &#34;pathname&#34;
        label = &#34;&#34;
        lightTheme = &#34;github-light&#34;
        darkTheme = &#34;github-dark&#34;
      # FixIt 0.2.13 | NEW Twikoo comment config (https://twikoo.js.org/)
      [params.page.comment.twikoo]
        enable = false
        envId = &#34;&#34;
        region = &#34;&#34;
        path = &#34;&#34;
        visitor = true
        commentCount = true
        # FixIt 0.2.17 | CHANGED enable lightgallery support
        lightgallery = false
        # FixIt 0.2.17 | NEW enable Katex support
        katex = false
      #  Giscus 评论系统设置
      [params.page.comment.giscus]
        enable = true
        repo = &#34;&#34;
        repoId = &#34;&#34;
        category = &#34;&#34;
        categoryId = &#34;&#34;
        mapping = &#34;pathname&#34;
        strict = &#34;0&#34; # 
        term = &#34;&#34;
        reactionsEnabled = &#34;1&#34;
        emitMetadata = &#34;0&#34;
        inputPosition = &#34;top&#34; # [&#34;top&#34;, &#34;bottom&#34;]
        lightTheme = &#34;light&#34;
        darkTheme = &#34;dark&#34;
        lazyLoad = true
    #  第三方库配置
    [params.page.library]
      [params.page.library.css]
        # someCSS = &#34;some.css&#34;
        # 位于 &#34;assets/&#34;
        # 或者
        # someCSS = &#34;https://cdn.example.com/some.css&#34;
      [params.page.library.js]
        # someJavascript = &#34;some.js&#34;
        # 位于 &#34;assets/&#34;
        # 或者
        # someJavascript = &#34;https://cdn.example.com/some.js&#34;
    #  页面 SEO 配置
    [params.page.seo]
      # 图片 URL
      images = [&#34;/favicon.ico&#34;]
      # 出版者信息
      [params.page.seo.publisher]
        name = &#34;Leehow&#34;
        logoUrl = &#34;/logo.png&#34;

  #  TypeIt 配置
  [params.typeit]
    # 每一步的打字速度（单位是毫秒）
    speed = 100
    # 光标的闪烁速度（单位是毫秒）
    cursorSpeed = 1000
    # 光标的字符（支持 HTML 格式）
    cursorChar = &#34;|&#34;
    # 打字结束之后光标的持续时间（单位是毫秒，&#34;-1&#34; 代表无限大）
    duration = -1
    #  打字完成后是否会连续循环
    loop = false

  #  Mermaid 配置
  [params.mermaid]
    # 取值详见 https://mermaid.js.org/config/theming.html#available-themes
    themes = [&#34;default&#34;, &#34;dark&#34;]

  # 盘古之白配置
  [params.pangu]
    # 适用于中文写作用户
    enable = true
    selector = &#34;article&#34; # 

  #  水印配置
  # 详细参数见 https://github.com/Lruihao/watermark#readme
  [params.watermark]
    enable = false
    # 水印内容（允许 HTML 格式）
    content = &#34;&#34;
    # 水印透明度
    opacity = 0.1
    # 水印父节点
    appendTo = &#34;.wrapper&gt;main&#34;
    # 单水印宽度 单位：px
    width = 150
    # 单水印高度 单位：px
    height = 20
    # 水印行间距 单位：px
    rowSpacing = 60
    # 水印列间距 单位：px
    colSpacing = 30
    # 水印旋转角度 单位：deg
    rotate = 15
    # 水印字体大小，单位：rem
    fontSize = 0.85
    #  水印字体
    fontFamily = &#34;inherit&#34;

  #  不蒜子统计
  [params.ibruce]
    enable = true
    # 在文章中开启
    enablePost = true

  # 网站验证代码，用于 Google/Bing/Yandex/Pinterest/Baidu/360/Sogou
  [params.verification]
    google = &#34;&#34;
    bing = &#34;&#34;
    yandex = &#34;&#34;
    pinterest = &#34;&#34;
    baidu = &#34;&#34;
    so = &#34;&#34;
    sogou = &#34;&#34;

  # FixIt 0.2.10 | 网站 SEO 配置
  [params.seo]
    # 图片 URL
    image = &#34;/favicon.ico&#34;
    # 缩略图 URL
    thumbnailUrl = &#34;favicon-32x32.png&#34;

  # FixIt 0.2.0 | NEW 网站分析配置
  [params.analytics]
    enable = true
    # Google Analytics
    [params.analytics.google]
      id = &#34;&#34;
      # 是否匿名化用户 IP
      anonymizeIP = true
    # Fathom Analytics
    [params.analytics.fathom]
      id = &#34;&#34;
      # 自行托管追踪器时的主机路径
      server = &#34;&#34;

  # FixIt 0.2.7 | NEW Cookie 许可配置
  [params.cookieconsent]
    enable = false
    # 用于 Cookie 许可横幅的文本字符串
    [params.cookieconsent.content]
      message = &#34;&#34;
      dismiss = &#34;&#34;
      link = &#34;&#34;

  # FixIt 0.2.7 | 第三方库文件的 CDN 设置
  [params.cdn]
    # CDN 数据文件名称，默认不启用 [&#34;jsdelivr.yml&#34;, &#34;unpkg.yml&#34;, ...]
    # 位于 &#34;themes/FixIt/assets/data/cdn/&#34; 目录
    # 可以在你的项目下相同路径存放你自己的数据文件：&#34;assets/data/cdn/&#34;
    # data = &#34;unpkg.yml&#34;

  # FixIt 0.2.8 | NEW 兼容性设置
  [params.compatibility]
    # 是否使用 Polyfill.io 来兼容旧式浏览器
    polyfill = false
    # 是否使用 object-fit-images 来兼容旧式浏览器
    objectFit = false

  # FixIt 0.2.14 | NEW 在左上角或者右上角显示 GitHub 开源链接
  [params.githubCorner]
    enable = false
    permalink = &#34;https://github.com/hugo-fixit/FixIt&#34;
    title = &#34;在 GitHub 上查看源代码&#34;
    position = &#34;right&#34; # [&#34;left&#34;, &#34;right&#34;]

  # FixIt 0.2.14 | NEW Gravatar 设置
  [params.gravatar]
    #  取决于作者邮箱，作者邮箱未设置则使用本地头像
    enable = true
    # Gravatar 主机，默认：“www.gravatar.com”
    host = &#34;cn.gravatar.com&#34; # [&#34;cn.gravatar.com&#34;, &#34;gravatar.loli.net&#34;, ...]
    style = &#34;identicon&#34; # [&#34;&#34;, &#34;mp&#34;, &#34;identicon&#34;, &#34;monsterid&#34;, &#34;wavatar&#34;, &#34;retro&#34;, &#34;blank&#34;, &#34;robohash&#34;]

  # FixIt 0.2.16 | NEW 返回顶部
  [params.backToTop]
    enable = true
    # 在 b2t 按钮中显示滚动百分比
    scrollpercent = true

  # FixIt 0.2.16 | NEW 阅读进度条
  [params.readingProgress]
    enable = true
    # 可用值：[&#34;left&#34;, &#34;right&#34;]
    start = &#34;left&#34;
    # 可用值：[&#34;top&#34;, &#34;bottom&#34;]
    position = &#34;top&#34;
    reversed = false
    light = &#34;&#34;
    dark = &#34;&#34;
    height = &#34;2px&#34;
  
  # FixIt 0.2.17 | NEW 页面加载期间顶部的进度条
  # 有关详细信息：https://github.com/CodeByZach/pace
  [params.pace]
    enable = false
    # 所有可用颜色：
    # [&#34;black&#34;, &#34;blue&#34;, &#34;green&#34;, &#34;orange&#34;, &#34;pink&#34;, &#34;purple&#34;, &#34;red&#34;, &#34;silver&#34;, &#34;white&#34;, &#34;yellow&#34;]
    color = &#34;blue&#34;
    # 所有可用主题：
    # [&#34;barber-shop&#34;, &#34;big-counter&#34;, &#34;bounce&#34;, &#34;center-atom&#34;, &#34;center-circle&#34;, &#34;center-radar&#34;, &#34;center-simple&#34;,
    # &#34;corner-indicator&#34;, &#34;fill-left&#34;, &#34;flash&#34;, &#34;flat-top&#34;, &#34;loading-bar&#34;, &#34;mac-osx&#34;, &#34;material&#34;, &#34;minimal&#34;]
    theme = &#34;minimal&#34;
  
  # FixIt 0.2.18-lts.3 | [试验性功能] 缓存图床图片到本地，详见：https://github.com/hugo-fixit/FixIt/pull/362
  [params.cacheRemoteImages]
    enable = false
    # 用本地图片链接替换远程图片链接
    replace = false
  
  # FixIt 0.2.17 | NEW 定义自定义文件路径
  # 在站点目录 `layouts/partials/custom` 中创建您的自定义文件，并取消注释下面需要的文件
  [params.customFilePath]
    # aside = &#34;custom/aside.html&#34;
    # profile = &#34;custom/profile.html&#34;
    # footer = &#34;custom/footer.html&#34;

  # FixIt 0.2.15 | NEW 开发者选项
  [params.dev]
    enable = false
    # 检查更新
    c4u = false
    # 请勿公开展示！
    githubToken = &#34;&#34;
    # 移动端开发者工具配置
    [params.dev.mDevtools]
      enable = false
      # 支持 &#34;vConsole&#34;, &#34;eruda&#34;
      type = &#34;vConsole&#34;

# -------------------------------------------------------------------------------------
# Modules Configuration
# See: https://gohugo.io/hugo-modules/configuration/#module-config-imports
# -------------------------------------------------------------------------------------

[module]
  [module.hugoVersion]
    extended = true
    min = &#34;0.110.0&#34;

# -------------------------------------------------------------------------------------
# Markup related configuration in Hugo
# See: https://gohugo.io/getting-started/configuration-markup/
# -------------------------------------------------------------------------------------

# Hugo 解析文档的配置
[markup]
  # 语法高亮设置 (https://gohugo.io/content-management/syntax-highlighting)
  [markup.highlight]
    ################## 必要的配置 ##################
    # https://github.com/hugo-fixit/FixIt/issues/43
    codeFences = true
    lineNos = true
    lineNumbersInTable = true
    noClasses = false
    ################## 必要的配置 ##################
    guessSyntax = true
  # Goldmark 是 Hugo 0.60 以来的默认 Markdown 解析库
  [markup.goldmark]
    [markup.goldmark.extensions]
      definitionList = true
      footnote = true
      linkify = true
      strikethrough = true
      table = true
      taskList = true
      typographer = true
    [markup.goldmark.renderer]
      # 是否在文档中直接使用 HTML 标签
      unsafe = true
  # Table Of Contents settings
  [markup.tableOfContents]
    startLevel = 2
    # endLevel = 4

# -------------------------------------------------------------------------------------
# Sitemap Configuration
# See: https://gohugo.io/templates/sitemap-template/#configuration
# -------------------------------------------------------------------------------------

# 网站地图配置
[sitemap]
  changefreq = &#34;daily&#34;
  filename = &#34;sitemap.xml&#34;
  priority = 0.5

# -------------------------------------------------------------------------------------
# Permalinks Configuration
# See: https://gohugo.io/content-management/urls/#permalinks
# -------------------------------------------------------------------------------------

# Permalinks 配置 (https://gohugo.io/content-management/urls#permalinks)
[Permalinks]
  # posts = &#34;:year/:month/:filename&#34;
  posts = &#34;/posts/:slug&#34;

# -------------------------------------------------------------------------------------
# Privacy Configuration
# See: https://gohugo.io/about/hugo-and-gdpr/
# -------------------------------------------------------------------------------------
# 隐私信息配置 (https://gohugo.io/about/hugo-and-gdpr/)
[privacy]
  [privacy.twitter]
    enableDNT = true
  [privacy.youtube]
    privacyEnhanced = true

# -------------------------------------------------------------------------------------
# Media Types
# See: https://gohugo.io/templates/output-formats/#media-types
# -------------------------------------------------------------------------------------

[mediaTypes]
  # 用于输出 Markdown 格式文档的设置
  [mediaTypes.&#34;text/markdown&#34;]
    suffixes = [&#34;md&#34;]
  # 用于输出 txt 格式文档的设置
  [mediaTypes.&#34;text/plain&#34;]
    suffixes = [&#34;txt&#34;]

# -------------------------------------------------------------------------------------
# Output Format Definitions
# See: https://gohugo.io/templates/output-formats/#output-format-definitions
# -------------------------------------------------------------------------------------

[outputFormats]
  # 用于输出 Markdown 格式文档的设置
  [outputFormats.MarkDown]
    mediaType = &#34;text/markdown&#34;
    isPlainText = true
    isHTML = false
  #  用于输出 baidu_urls.txt 文件的设置
  [outputFormats.BaiduUrls]
    baseName = &#34;baidu_urls&#34;
    mediaType = &#34;text/plain&#34;
    isPlainText = true
    isHTML = false

# -------------------------------------------------------------------------------------
# Customizing Output Formats
# See: https://gohugo.io/templates/output-formats/#customizing-output-formats
# -------------------------------------------------------------------------------------
#  用于 Hugo 输出文档的设置
[outputs]
  home = [&#34;HTML&#34;, &#34;RSS&#34;, &#34;JSON&#34;, &#34;BaiduUrls&#34;]
  page = [&#34;HTML&#34;]
  section = [&#34;HTML&#34;, &#34;RSS&#34;]
  taxonomy = [&#34;HTML&#34;, &#34;RSS&#34;]
  taxonomyTerm = [&#34;HTML&#34;]

# -------------------------------------------------------------------------------------
# Taxonomies Configuration
# See: https://gohugo.io/content-management/taxonomies/#configure-taxonomies
# -------------------------------------------------------------------------------------

[taxonomies]
  # series = &#34;series&#34;
  category = &#34;categories&#34;
  tag = &#34;tags&#34;
  collections = &#34;collections&#34;

```

![hugo配置文件](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202312142004055.png)

#### 修改文章前缀模板
在每篇 markdown 文章最前面可以用一部分注释来告诉`FixIt主题`，这篇文章的属性，譬如文章标签、分类、是否为草稿等。
&gt;详细可参考 [FixIt 官方文档](https://fixit.lruihao.cn/zh-cn/documentation/content-management/introduction/#front-matter)

用下面的内容覆盖`archetypes/default.md` 以及 `archetypes/posts.md`文件。
**注意：实际使用的时候要把摘要的斜杠去掉**
```yaml
---
title: &#34;{{ replace .TranslationBaseName &#34;-&#34; &#34; &#34; | title }}&#34;
slug: &#34;{{ replace .TranslationBaseName &#34;_&#34; &#34;-&#34; | title }}&#34;
# 副标题
subtitle: &#34;&#34;
# 文章描述，是搜索引擎呈现在搜索结果链接下方的网页简介，建议设置
description: &#34;&#34;
date: {{ .Date }}
lastmod: {{ .Date }}
# 文章过期提醒
outdatedInfoWarning: true
draft: false

# 文章的标签
tags:
- 

# 文章所属的类别
categories:
- 

# 文章所属的合集
collections:
-

# 是否在侧边栏开启合集
collectionList: true
# 是否在帖子末尾启用合集
collectionNavigation: true

# 如果设为 true, 这篇文章将不会显示在主页上
hiddenFromHomePage: false
# 如果设为 true, 这篇文章将不会显示在搜索结果中
hiddenFromSearch: false

# 文章的特色图片
featuredImage: &#34;&#34;
# 用在主页预览的文章特色图片
featuredImagePreview: &#34;&#34;

license: &#39;&lt;a rel=&#34;license external nofollow noopener noreffer&#34; href=&#34;https://creativecommons.org/licenses/by-nc/4.0/&#34; target=&#34;_blank&#34;&gt;CC BY-NC 4.0&lt;/a&gt;&#39;
---

此处内容将会出现在摘要（summary）里

&lt;!--\more--&gt; # 此处的“\”用于转义，否则无法正常显示，实际使用须删去。

此处开始为正文

```

![文章前缀模板](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202312142018958.png)

### 创建你的第一篇文章
以下是创建新文章的命令：
```bash
hugo new posts/文章标题.md
```
执行完成后，在`./content/posts`目录下应该可以看到新文件，同时里面已经有 markdown 模版中的文章前缀参数。
你可以在`VScode`中随意编辑文章。
![创建出的新文章](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202312142019979.png)

### 本地调试
```bash
hugo serve -D --disableFastRender
```
![本地调试](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311081636839.png)

浏览器中打开 [http://localhost:1313/](http://localhost:1313/)，就能看到网站效果。
![网站效果](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311081636924.png)
## Github
### 在 Windows 上创建 SSH 密钥并将其添加到 GitHub
#### Windows 端生成 SSH 密钥
使用 Git Bash 或命令行打开终端窗口，输入以下命令。记得把`your_email@example.com`改成你自己的邮箱地址。
```bash
ssh-keygen -t rsa -b 4096 -C &#34;your_email@example.com&#34;
```
按照提示键入您想要保存密钥的文件名和路径，或使用默认设置。
![生成SSH密钥](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311081637024.png)
接下来，系统将生成一个随机字符串作为密钥密码。此处可以选用默认密码以便于不需要输入密码进行 SSH 登录。进入生成密钥的文件夹，查看密钥：
![查看密钥](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311081637119.png)
#### 添加到 GitHub
1. 登录到 GitHub 账户，并转到“Settings”（设置）中的“SSH and GPG keys”（SSH 和 GPG 密钥）页面。
2. 点击“New SSH key”（新建 SSH 密钥），填写标题和密钥的内容。
![新建 SSH 密钥](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311081637219.png)

1. 打开`id_rsa.pub`公钥文件 (即你在生成的时候保存的文件) ，将其内容复制到 GitHub 的 “Key” 字段中。
2. 最后，点击“Add SSH key” （添加 SSH 密钥），完成密钥添加。
![添加 SSH 密钥](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311081637309.png)
### 创建 blog 仓库
用于存储博客源文件，也就是刚才的本地项目文件。
1. 在 GitHub 网站上登录你的账号，然后点击页面右上角的加号图标，选择 &#34;New repository&#34;（新建仓库）。
2. 在 &#34;Initialize this repository with&#34;（使用以下方式初始化仓库）部分，选择 &#34;Add a README file&#34;（添加一个 README 文件）选项。
3. 暂存并提交现有文件
```bash
git add . 
git commit -m &#34;init blog files&#34;
```
4. 点击 &#34;Create repository&#34;（创建仓库）按钮，完成 GitHub 仓库的创建。
![创建 blog 仓库](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311081637388.png)

5. 将本地仓库与远程 GitHub 仓库关联起来。在项目目录中打开 Git Bash，执行以下命令，将 `&lt;remote-url&gt;` 替换为你的 GitHub 仓库的远程 URL：
```bash
git remote add origin &lt;remote-url&gt;
```
例如：
```bash
git remote add origin https://github.com/your-username/your-repository.git
```
6. 将本地代码推送到远程仓库的 main 分支。执行以下命令：
```bash
git push -u origin main
```
这将把本地的代码推送到远程仓库的 `main` 分支，并将其设置为默认上游分支。
### 创建 Github Pages 公开仓库
用于实际展示博客。
1. 创建新仓库
![创建新Github Pages仓库](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311081637474.png)

2. `Repository name` 这里一定要填 `[你的github账号].github.io`。`你的github账号`必须小写字母。仓库可见性设为`Public`。选择“使用 README 初始化此存储库”。
![新建Github Pages仓库](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311081637559.png)
### 上传页面
##### 进入项目根目录，执行：
```bash
hugo
```
执行后，站点根目录下会生成一个 `public` 文件夹，该文件下的内容即 Hugo 生成的整个静态网站。每次更新内容后，将 `pubilc` 目录里所有文件 push 到 GitHub Pages 所在的仓库即可。
##### 上传代码至 master
首次使用的时候要执行以下命令：
```shell
cd public
git init
git remote add origin https://github.com/leegical/leegical.github.io.git # 将本地目录链接到远程服务器的代码仓库
git add .
git commit -m &#34;[介绍，随便写点什么，比如日期]&#34;
git push -u origin master
```

##### 更改 Pages 展示分支
进入 Github Pages 仓库的`Setting`-`Pages`，把`Branch`修改为`master`，点击 save。
![修改发布Branch](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311081637645.png)

稍等几分钟即可通过`[你的github账号].github.io`来访问博客站点了，和`hugo serve -D`本地调试完全一致。
### Github Action 自动发布
通过上述命令我们可以手动发布我们的静态文件，但还是有以下弊端：
1. 发布步骤还是比较繁琐，本地调试后还需要切换到 `public/` 目录进行上传
2. 无法对博客 `.md` 源文件进行备份与版本管理
可以通过官方提供的 GitHub Action 进行 CI 自动发布。
#### 增加 action 配置文件
回到 blog 仓库的本地文件夹，新增`.github/workflows/deploy.yml`
```bash
mkdir .github
mkdir .github/workflows
touch .github/workflows/deploy.yml
```
![新建deploy.yml](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311081637741.png)

用 vscode 编辑 deploy.yml 的内容，参考如下：
```yml
name: deploy  

on:
    push:
    pull_request:
    workflow_dispatch:
    schedule:
        # Runs everyday at 0:00 AM
        - cron: &#34;0 0 * * *&#34;

jobs:
    build:
        runs-on: ubuntu-latest
        steps:
            - name: Checkout
              uses: actions/checkout@v2
              with:
                  submodules: true
                  fetch-depth: 0

            - name: Setup Hugo
              uses: peaceiris/actions-hugo@v2
              with:
                  hugo-version: &#34;latest&#34;
                  extended: true  

            - name: Build Web
              run: hugo

            - name: Deploy Web
              uses: peaceiris/actions-gh-pages@v3
              with:
                  PERSONAL_TOKEN: ${{ secrets.PERSONAL_TOKEN }}
                  EXTERNAL_REPOSITORY: leegical/leegical.github.io
                  PUBLISH_BRANCH: master
                  PUBLISH_DIR: ./public
                  commit_message: ${{ github.event.head_commit.message }}
```

注意：`EXTERNAL_REPOSITORY`要修改为 Github Pages 的链接
![deploy.yml](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311081637836.png)

提交变更到 Github：
```bash
git add .
git commit -m &#34;add action config&#34;
git push
```
![提交变更](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311081637929.png)
#### 设置 action 变量
进入 [Github tokens](https://github.com/settings/tokens) ，点击`Generate new token`——`Generate new token (classic)`
![Generate new token](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311081637020.png)

- Note：随便写
- Expiration：`No expiration`
- Select scopes：只勾选 `repo`
![设置属性](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311081637107.png)
拉到最下面，点击生成。
![生成密钥](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311081637199.png)

注意生成的 token 只会显示这一次，形如 `ghp_xxxxxxxxxx`，点击复制。
回到 blog 仓库——Setting，新建仓库密钥
![新建仓库密钥](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311081637293.png)

- Name：PERSONAL_TOKEN
- Secret：填刚才复制的密钥
![粘贴密钥](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311081637376.png)
## 自定义博客域名
`你的github账户名.github.io`的网址在国内访问速度较慢，为博客设置一个自定义域名可以有效加快速度。以本博客为例，要设置的自定义域名为：`haoyep.com`。
### Cloudflare 配置
1. 使用 Cloudflare 托管域名，这一点教程很多，跟着做就行。
![托管域名](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202312141651245.png)

2. 在 DNS 配置中，新增一条 CNAME 解析记录到`你的github账户名.github.io`，不启用代理。
![新增一条 CNAME 解析记录](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202312142035444.png)

### hugo 配置
1. 在 `static` 中添加 CNAME 文件，内容为自定义域名为 `haoyep.com`。
![CNAME 文件](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202312142031955.png)

2. `hugo.toml` 修改 `baseURL` 为自定义域名为 `haoyep.com`。
![baseURL](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202312142033201.png)

提交到 Github 仓库
```bash
hugo
git add .
git commit -m &#34;Create CNAME&#34;
git push
```
### Github Pages 仓库配置
为自定义域名启用 SSL 证书。
Settings——Pages——Custom domain，勾选 **Enforce HTTPS**。
![](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202312142041938.png)

## 总结
以上整个环境部署好之后，接下来的常用命令就是以下几个：
- 1. **站点目录**下，新建文章，执行：
```bash
hugo new posts/文章名.md
```
- 2. 使用`VScode`编辑文章内容或修改，包括修改主题之类的。在本地进行调试:
```bash
hugo serve -D --disableFastRender
```
- 3. 修改完成，确定要上传到 GitHub 上后，**站点目录**下执行：
```bash
hugo
```
进行编译，没错误的话修改的内容就顺利同步到`public`下了，然后执行提交命令：
```shell
git add .
git commit -m &#34;随便写点提交信息&#34;
git push
```
稍等片刻，github action 执行完毕，页面就会更新了。
## [选择和配置 Hugo 主题](https://hugoloveit.com/zh-cn/theme-documentation-basics/)
### 网站 logo
在本地项目文件夹`static`中添加2个方形 png 图片，命名为`avatar.png`、`logo.png`，作为网站头像和 logo：
![网站头像和 logo](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311081638404.png)

并修改`hugo.toml`文件中对应的参数。
### 网站小图标
我是在这个[网站](https://bigheads.io/editor/?accessory=shades&amp;body=chest&amp;circleColor=blue&amp;clothing=dressShirt&amp;clothingColor=red&amp;eyebrows=concerned&amp;eyes=happy&amp;faceMask=false&amp;faceMaskColor=white&amp;facialHair=none&amp;graphic=none&amp;hair=none&amp;hairColor=blue&amp;hat=beanie&amp;hatColor=blue&amp;lashes=false&amp;lipColor=turqoise&amp;mask=false&amp;mouth=openSmile&amp;skinTone=light)上生成自己的 svg 小图标。然后把文件下载后，放在博客的`static`目录中。
![网站svg图标](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202312142045154.png)

前往[这个网站](https://realfavicongenerator.net/)，生成下面的文件：
- apple-touch-icon.png (180x180)
- favicon-32x32.png (32x32)
- favicon-16x16.png (16x16)
- mstile-150x150.png (150x150)
- android-chrome-192x192.png (192x192)
- android-chrome-512x512.png (512x512)
然后放在 `/static` 目录。

并修改`hugo.toml`文件中对应的参数。

记得提交更改
```bash
git add .
git commit -m &#34;修改主题&#34;
git push
```
稍等片刻，github action 执行完毕，页面就会更新了。

---

> 作者: [Leehow](https://www.haoyep.com/)  
> URL: https://www.haoyep.com/posts/windows-hugo-blog-github/  


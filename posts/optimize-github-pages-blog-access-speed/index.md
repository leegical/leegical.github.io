# Github Pages 博客网站访问速度优化

个人博客访问速度优化记录。使用自定义域名、分流CDN等方法实现加快加载速度。

&lt;!--more--&gt;

使用 Github Pages 可以方便地搭建自己的静态网站，详细过程参考我的这篇文章。
{{&lt; link &#34;https://www.haoyep.com/posts/windows-hugo-blog-github/&#34; &#34;使用 hugo 和 Github Pages 搭建个人博客&#34; &#34;使用 hugo 和 Github Pages 搭建个人博客&#34; true &gt;}}

但由于众所周知的原因，此方法搭建的博客在国内访问速度不佳。因此考虑采用一些方法来加速访问，主要思路是使用 CDN 加速网站的静态资源。

对于不同的静态资源，加速方法分别如下：

1. 使用自定义域名，见[个人 Github 博客设置自定义域名](https://www.haoyep.com/posts/windows-hugo-blog-github/#%E8%87%AA%E5%AE%9A%E4%B9%89%E5%8D%9A%E5%AE%A2%E5%9F%9F%E5%90%8D)；
2. `js/css`文件
	- ~~使用`jsdelivr` 和 `unpkg` 进行 CDN 加速~~，亲测使用自定义域名后，这两个 CDN 反而会降速。因此不需要单独对`js/css`文件加速。
3. 托管在 Github 仓库上的[图床图片](#图片加速)。
	- 本人博客上的图片都是使用 PicGo 上传到图床，图床是用 GitHub 仓库搭建的，见[图床搭建过程](https://www.haoyep.com/posts/github-graph-beds) 。为了加快 GitHub 文件访问速度，参考[通过 Cloudflare 和 jsDelivr 免费加速博客 GitHub 图床等静态资源](https://www.haoyep.com/posts/github-graph-beds-cdn/)，通过自定义域名区分国内外请求，分配不同的 CDN 资源。最后，替换博客内所有 Github 文件链接即可。
![替换 Github 文件链接](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202312152140943.png)
4. [加速谷歌字体](#加速谷歌字体)
5. [加速 avatar 头像](#加速-avatar-头像)

## 图片加速
首先参考这篇文章，搭建加速域名。
{{&lt; link &#34;https://www.haoyep.com/posts/github-graph-beds-cdn/&#34; &#34;通过 Cloudflare 和 jsDelivr 免费加速博客 GitHub 图床等静态资源&#34; &#34;通过 Cloudflare 和 jsDelivr 免费加速博客 GitHub 图床等静态资源&#34; true &gt;}}

对于要使用的图片，使用 PicGo 上传到 GitHub 图床，获取 CDN 加速链接。然后在配置文件中使用相应的链接即可。下面介绍几个配置中常见的图片。

### 网站图片
```toml
# 网站图片，用于 Open Graph 和 Twitter Cards
  images = [&#34;https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/weblogo.png&#34;]
```
![网站图片，用于 Open Graph 和 Twitter Cards](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202312161421814.png)
### 网站图标
配置：`[params]`——`[params.app]`。
```toml
# 应用图标配置
  [params.app]
    # 当添加到 iOS 主屏幕或者 Android 启动器时的标题，覆盖默认标题
    title = &#34;云吱&#34;
    # 是否隐藏网站图标资源链接
    noFavicon = false
    # 更现代的 SVG 网站图标，可替代旧的 .png 和 .ico 文件
    svgFavicon = &#34;https://cdn.haoyep.com/gh/leegical/Blog_img/favicon.svg&#34;
```
![网站图标](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202312161426248.png)

### 网站 logo
配置：`[params]`——`[params.header]`——`[params.header.title]`。
```toml
#  页面头部导航栏标题配置
    [params.header.title]
      # LOGO 的 URL
      logo = &#34;https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/weblogo.png&#34;
```
![网站 logo](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202312161428936.png)
### 主页头像
配置：`[params]`——`[params.home]`——`[params.home.profile]`。
```toml
# 主页个人信息
    [params.home.profile]
      enable = true
      # Gravatar 邮箱，用于优先在主页显示的头像
      gravatarEmail = &#34;&#34;
      # 主页显示头像的 URL
      avatarURL = &#34;https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/avatar.png&#34;
```
![主页头像](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202312161433480.png)
## 加速谷歌字体
[**FixIt** 主题](https://github.com/hugo-fixit/FixIt)默认使用系统字体作为博客渲染字体，免去了加载字体。
![Fixit主题全局字体](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202312152148953.png)

但是想要为一些特定区域，如 `code` 设置特别字体时，就需要用到谷歌字体。这里选择使用 `fonts.loli.net` 加速。在 `assets/css` 中新建 `_override.scss` 文件，内容如下：
```scss
@import url(&#39;https://fonts.loli.net/css?family=JetBrains&#43;Mono:400,700&amp;display=swap&amp;subset=latin-ext&#39;);
$code-font-family: JetBrains Mono, Fira Mono, Source Code Pro, Menlo, Consolas, Monaco, monospace;
```
![加速code的谷歌字体](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202312152151358.png)

## 加速 avatar 头像
在 `hugo.toml` 设置 Gravatar 主机为七牛云地址 `dn-qiniu-avatar.qbox.me`：
```toml
  # FixIt 0.2.14 | NEW Gravatar 设置
  [params.gravatar]
    #  取决于作者邮箱，作者邮箱未设置则使用本地头像
    enable = true
    # Gravatar 主机，默认：“www.gravatar.com”
    host = &#34;dn-qiniu-avatar.qbox.me&#34; # [&#34;cn.gravatar.com&#34;, &#34;gravatar.loli.net&#34;, ...]
    style = &#34;identicon&#34; # [&#34;&#34;, &#34;mp&#34;, &#34;identicon&#34;, &#34;monsterid&#34;, &#34;wavatar&#34;, &#34;retro&#34;, &#34;blank&#34;, &#34;robohash&#34;]
```
![设置 Gravatar 主机为七牛云地址](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202312152153926.png)


---

> 作者: [云吱](https://www.haoyep.com/)  
> URL: https://www.haoyep.com/posts/optimize-github-pages-blog-access-speed/  


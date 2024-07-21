# 通过 Cloudflare 和 jsDelivr 免费加速博客 GitHub 图床等静态资源


通过 Cloudflare 和 jsDelivr 免费加速博客 GitHub 静态资源(GitHub图床)，自动实现 CDN 资源的海内外分流，加速博客访问速度。

&lt;!--more--&gt;

## 前言
上一篇文章讲述了如何使用 PicGo &#43; GitHub 搭建图床，这样搭建的图床很稳定，但缺点是国内访问速度慢。可以使用 `jsDelivr` 对 Github 图床等静态资源进行免费 CDN 加速
{{&lt; link &#34;https://www.haoyep.com/posts/github-graph-beds/&#34; &#34;使用PicGo &#43; GitHub 搭建 Obsidian 图床&#34; &#34;使用PicGo &#43; GitHub 搭建 Obsidian 图床&#34; true &gt;}}

{{&lt; admonition question &#34;jsDelivr是什么？&#34; &gt;}}
`jsDelivr`是国外的一家优秀的公共 CDN 服务提供商，该平台是首个「打通中国大陆与海外的免费 CDN 服务」，无须担心中国防火墙问题而影响使用。官网：[http://www.jsdelivr.com/(opens new window)](http://www.jsdelivr.com/)
{{&lt; /admonition &gt;}}

但是`jsDelivr`因为掉 ICP 等原因，国内速度越来越慢。好在 [Chinajsdelivr](https://github.com/54ayao/Chinajsdelivr) 项目将它在国内“复活”了。

因此，本文思路是，对于 Github 公开仓库中的静态资源：
- 如果访问来源是国内，则使用 [Chinajsdelivr](https://github.com/54ayao/Chinajsdelivr) 进行加速，域名为`jsd.cdn.zzko.cn`
- 如果访问来源是国内，则使用原版 jsDelivr 进行加速，域名为`cdn.jsDelivr.net`

即：
```
# 1-1. Github raw 链接
https://raw.githubusercontent.com/leegical/Blog_img/main/md_img202305061640828.png
# 1-2. Github 仓库文件链接
https://github.com/leegical/Blog_img/blob/main/md_img202305061640828.png

# 国内请求将访问到
https://jsd.cdn.zzko.cn/gh/leegical/Blog_img/md_img202305061640828.png

# 国外请求将访问到
https://cdn.jsdelivr.net/gh/leegical/Blog_img/md_img202305061640828.png
```

也就是说，我希望对于同一个资源链接，能够根据国内外请求来源自动重定向，使用不同的 CDN 加速链接。这就可以使用 Cloudflare 的重定向规则。
## Cloudflare
### 配置域名
使用 Cloudflare 托管域名，这一点教程很多，跟着做就行，
![托管域名](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202312141651245.png)

在 DNS 配置中，新增一条 CNAME 解析记录，并启用代理。
如图，我这里是将 `cdn.haoyep.com` 解析到了 `jsd.cdn.zzko.cn`，并使用 Cloudflare 代理（点亮小云朵）。
![添加CNAME解析记录](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202312141652319.png)

### 配置重定向规则
**目标**：资源链接都使用 `cdn.haoyep.com`，Cloudflare 在代理 `cdn.haoyep.com` 时，判断请求来源是国内，则将 `cdn.haoyep.com` 重定向到 `jsd.cdn.zzko.cn`；国外的请求则重定向到 `cdn.jsdelivr.net`。

1. 配置国内重定向
	- 规则名称 （必需）：标注国内，方便区分
	- 自定义筛选表达式：`(http.host eq &#34;cdn.haoyep.com&#34; and ip.geoip.country eq &#34;CN&#34;)`
	- URL 重定向
		- 类型：动态
		- 表达式：`concat(&#34;https://jsd.cdn.zzko.cn&#34;, http.request.uri.path)`
		- 状态代码：`302`

![国内重定向规则配置](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202312141658616.png)

2. 配置国外重定向
	- 规则名称 （必需）：标注国外，方便区分
	- 自定义筛选表达式：`(http.host eq &#34;cdn.haoyep.com&#34; and ip.geoip.country ne &#34;CN&#34;)`
	- URL 重定向
		- 类型：动态
		- 表达式：`concat(&#34;https://cdn.jsdelivr.net&#34;, http.request.uri.path)`
		- 状态代码：`302`

![国外重定向规则配置](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202312141700130.png)

{{&lt; admonition tip &gt;}}
HTTP 重定向状态选择302而不是301。虽然两类请求都会被 Cloudflare 缓存，但301理论上是永久跳转而302是临时跳转，因此301可能会导致长时间缓存，不利于今后修改重定向到新地址。
{{&lt; /admonition &gt;}}
## PicGo 设置
为了让上传的图片自动生成 CDN 链接，还需要配置 PicGo：
![PicGo Github 图床设置](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202312141324478.png)
- 设定存储路径：可以不填，也可以填仓库的某个文件夹
- 自定义域名： 改为`https://&lt;cdn加速链接&gt;/gh/&lt;用户名&gt;/&lt;图床仓库名&gt;`，如图我这里改成 `https://cdn.haoyep.com/gh/leegical/Blog_img` 即可。

对于之前文章中的 Github raw 或文件链接，替换成 CDN 链接即可。本文只需要进行以下替换：
```
# 要替换的
https://raw.githubusercontent.com/leegical/Blog_img/main
https://github.com/leegical/Blog_img/blob/main

# 替换为
https://cdn.haoyep.com/gh/leegical/Blog_img
```

## 参考文章
{{&lt; link &#34;https://github.com/54ayao/Chinajsdelivr?tab=readme-ov-file&#34; &#34;Chinajsdelivr简介&#34; &#34;Chinajsdelivr简介&#34; true &gt;}}

{{&lt; link &#34;https://upup.dev/posts/cloudflare-country-based-cdn-redirect/&#34; &#34;利用 Cloudflare 重定向规则实现 CDN 资源的海内外分流&#34; &#34;利用 Cloudflare 重定向规则实现 CDN 资源的海内外分流&#34; true &gt;}}

{{&lt; link &#34;https://irithys.com/p/%E4%BD%BF%E7%94%A8npm%E5%8A%A0%E9%80%9F%E9%9D%99%E6%80%81%E8%B5%84%E6%BA%90/&#34; &#34;使用npm加速静态资源&#34; &#34;使用npm加速静态资源&#34; true &gt;}}


---

> 作者: [Leehow](https://www.haoyep.com/)  
> URL: https://www.haoyep.com/posts/github-graph-beds-cdn/  


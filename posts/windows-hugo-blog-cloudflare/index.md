# Windows 下使用 Hugo 和 Cloudflare Pages 配置博客


使用 Hugo 和 Cloudflare Pages 配置博客，自定义域名并启用SSL，还可以白嫖Cloudflare的CDN。

&lt;!--more--&gt;

{{&lt; admonition warning &#34;更新于2023-12-14&#34; &gt;}}
经过测试，在开启自定义域名时，Cloudflare Pages 在国内的访问速度远慢于 Github Pages。因此建议还是使用 Github Pages。
{{&lt; /admonition &gt;}}

{{&lt; link &#34;https://www.haoyep.com/posts/windows-hugo-blog-github/&#34; &#34;使用hugo和Github Pages配置博客&#34; &#34;使用hugo和Github Pages配置博客&#34; true &gt;}}

## 前言
如果懒得使用 Github Pages 以及配置 Github Action，又想用自定义域名和 cdn 加速访问博客，那么 hugo &#43; Cloudflare Pages 绝对是不二之选。
**准备工作：** 参考 [Windows 下使用 hugo 和 Github Pages 配置博客](https://www.haoyep.com/posts/windows_hugo_github_pages_blog/)，从头开始配置，一直到完成 [创建 blog 仓库](https://www.haoyep.com/posts/windows_hugo_github_pages_blog/#2%E5%88%9B%E5%BB%BA-blog-%E4%BB%93%E5%BA%93)。
## 设置 Cloudflare Pages
### 新建 Pages
登录 cloudflare，点击左侧的`Workers和Pages`，选择`Pages`——连接到 Git
![image.png](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311081549200.png)

允许 cloudflare 访问 blog 仓库，选择这个仓库开始设置。
![image.png](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311081550760.png)

### 设置构建环境
- 项目名称：随便写，之后会分配给你一个`[项目名称].pages.dev`。我这里就是 `leev.pages.dev`
- 生产分支：一般默认选择 main
- 框架预设：hugo
- 环境变量
	- 设置 hugo 版本，设置成当前最新版本。我这里是：HUGO_VERSION=0.120.3
	- 开启 hugo 扩展功能，extend=true
![image.png](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311081553496.png)
### 部署成功
通过`[项目名称].pages.dev`访问站点
![image.png](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311081556682.png)


## 设置域名
### 首先自行添加个人域名
![image.png](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311081559407.png)

### 绑定域名
- 进入构建好的 Pages
![image.png](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311081600461.png)
- 自定义域——设置自定义域
![image.png](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311081601828.png)
- 添加自定义域。可以设置一级或二级域名，这里我直接用了一级域名
![image.png](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311081602294.png)
![image.png](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311081603622.png)

然后进入 Pages，绑定域名。
![image](https://img.allworldg.xyz/2022/05/4b4a00bb92c5985a9e60925c9e3c7426.png)
- 等待片刻，DNS 解析生效
![image.png](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311081604721.png)
## 成果展示
现在可以直接通过自定义域名访问博客了，而且自动有 SSL。
例如现在就可以通过 [https://www.haoyep.com/](https://www.haoyep.com/) 来访问Leehow的小站啦~
![image.png](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311081606080.png)

## 总结
以上整个环境部署好之后，接下来的常用命令就是以下几个：
- 1. **站点目录**下，新建文章，执行：
```bash
hugo new posts/文章名.md
```
- 2. 使用`VScode`编辑文章内容或修改，包括修改主题之类的。在本地进行调试:
```bash
hugo serve -D
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
之后 Cloudflare 就会自动拉取、构建网站。

---

> 作者: [Leehow](https://www.haoyep.com/)  
> URL: https://www.haoyep.com/posts/windows-hugo-blog-cloudflare/  


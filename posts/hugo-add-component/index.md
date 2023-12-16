# Hugo 博客添加 Giscus 评论功能

本文主要记录了如何引入 giscus 为博客添加评论功能。用户登陆Github账号后即可评论文章。
<!--more-->

>参考知乎 [Hugo 的 LoveIt 主题添加 Giscus 评论](https://zhuanlan.zhihu.com/p/642438343)：Giscus 是一个由 Github Discussions 驱动的评论系统，无需自己单独配置，直接白嫖 Github 的资源即可，而且 UI 和功能都十分地合适我，配合 LoveIt 的配置还可以做到十分美观。

## 配置 Github 仓库
进入 Github Pages 仓库，找到`Settings -> General -> Features -> Discussions` 勾选，为仓库启动 Discussions 功能
![image.png](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311081213743.png)

## 安装 Giscus
- 点击[这里](https://github.com/apps/giscus)，我们将会看到下面的界面，我们点击`Install`
![image.png](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311081216731.png)

- 点击安装后，依次选择`Only select repositories`——`Select repositories`——选择 Github Pages 仓库。点击`Install`安装。
![image.png](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311081217166.png)
## 配置 Giscus
接下来，我们只需到 Giscus 官网获取配置信息，然后将配置信息填到 Hugo 的配置文件中即可。但是由于主题的不同，所以配置文件的填写也不同，这里以 LoveIt 为例。
### 来到 [Giscus 官网](https://giscus.app/zh-CN)
- 仓库：填写 Github Pages 仓库名
- 页面 ↔️ discussion 映射关系：**Discussion 的标题包含页面的 `pathname`**
- Discussion 分类：Announcements
![image.png](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311081221150.png)
- 其他选项默认。往下滑，找到配置文件。记下`data-repo`，`data-repo-id`，`data-category`，`data-category-id`，`data-mapping`这几个值。
![image.png](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311081226064.png)
### 修改 Hugo 配置
使用 vscode 打开 blog 仓库的本地项目文件夹，修改`hugo.toml`。在[params]——[params.page]处添加评论功能：
```toml
[params.page.comment]
      enable = true
      # giscus comment 评论系统设置 (https://giscus.app/zh-CN)
      [params.page.comment.giscus]
        # 你可以参考官方文档来使用下列配置
        enable = true
        repo = "leegical/leegical.github.io"
        repoId = "R_kxxxx"
        category = "Announcements"
        categoryId = "DIC_kxxxx"
        # 为空时自动适配当前主题 i18n 配置
        lang = ""
        mapping = "pathname"
        reactionsEnabled = "1"
        emitMetadata = "0"
        inputPosition = "bottom"
        lazyLoading = false
        lightTheme = "light"
        darkTheme = "dark"
```
![image.png](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311081236503.png)

### 提交更改
```bash
git add .
git commit -m "add comment func"
git push
```
稍等片刻，Github Action 会自动更改。

用户登录 Github 后即可评论，效果图如下：
![image.png](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311081302484.png)


---

> 作者: [云吱](https://haoyep.com/)  
> URL: https://haoyep.com/posts/hugo-add-component/  


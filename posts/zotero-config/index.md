# 文献管理软件 zotero 下载安装使用与配置分享


## 前言
最开始阅读文献是使用[readpaper 平台]( https://readpaper.com/ "readpaper 平台")，在线翻译、做笔记、文献管理都很方便，具体使用可以参考[同济子豪兄]( https://www.bilibili.com/video/BV1dg411P7De "同济子豪兄")和[官方 ReadPaper 保姆级教程]( https://www.bilibili.com/video/BV13T411V7rN "官方 ReadPaper 保姆级教程")。

但随着科研深入，readpaper 的文献管理功能逐渐跟不上了，而且很多文献没有 PDF 文件，需要自己下载后上传。

经过研究发现，相比 Endnote，zotero 功能够用，而且**开源**。通过插件也可以实现 readpaper 的在线翻译功能，配合 snipaste 软件可以截图固定，非常 nice！
>【注】本文参考了[知乎专栏]( https://zhuanlan.zhihu.com/p/347493385 "知乎专栏")。

## 下载安装
### 蓝奏云
官网访问困难的，可以点击[蓝奏云]( https://hzyy.lanzoux.com/b0e4ci3bi "蓝奏云")链接下载，_更新于2023-11-8_
>密码:2333

![image](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311071323017.png)


### 官网下载
#### 本体[Zotero 下载]( https://www.zotero.org/ "Zotero 下载")
Zotero 官网访问速度慢的，建议使用蓝奏云中`Zotero-6.0.18_setup.exe`进行安装。
#### 浏览器插件：[Zotero Connector]( https://www.zotero.org/download/connectors "Zotero Connector")下载
#### 翻译器：[Zotero translators_CN]( https://github.com/l0o0/translators_CN "Zotero translators_CN")下载
Zotero 官网访问速度慢的，建议下载蓝奏云中的`translators.zip`。
#### 插件
- zotero 官方插件下载地址： https://www.zotero.org/support/plugins
- zotero 中文社区推荐插件： https://plugins.zotero-chinese.com/#/
访问速度慢的，建议下载蓝奏云中`插件.zip`，压缩包里包含本文全部插件。
{{< admonition tip >}}
强烈建议下载[Zotero 插件合集](https://github.com/syt2/zotero-addons)，这个插件可以帮你自动管理、更新zotero插件。
![image.png](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311082226948.png)
{{< /admonition >}}
##### 插件安装
- 方法一：
打开【Zotero】
点击【工具】—【插件】
点击右上角【⚙】—【Install Add-on From File…】—选中需要安装的插件（部分插件不适用该方法）
安装完毕后重启【Zotero】
![image](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311071323817.png)
![image](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311071535599.png)
![image](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311071323892.png)
![image](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311071323977.png)
![image](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311071323064.png)

- 方法二：
打开【Zotero】
点击【工具】—【插件】
将需要安装的插件【拖动】至该页面
安装完毕后重启【Zotero】

按需启用插件。我的插件启用情况如下：
![image](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311071536098.png)

## 基础配置
打开【Zotero】—【编辑】—【首选项】
### 高级
#### 更改数据存储位置
安装完 zotero 后，第一件事就是更改数据存储位置。因为以后要存 PDF 文献，所以建议放在一个存储空间充裕的地方。改完位置后点击 OK 保存，重启 zotero 生效。
![image](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311071537731.png)

#### 添加搜索引擎
1. 【Zotero】—【编辑】—【首选项】— 文件和文件夹 —【打开数据文件夹】
![image](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311071537485.png)
2. locate — 打开`engines.json`文件
![image](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311071538437.png)
3. 编辑`engines.json`文件，将里面的内容全选删除，粘贴为以下内容并保存。

```json
[
	{
		"_name": "熊猫学术",
		"_alias": "panda",
		"_description": "谷歌学术镜像",
		"_icon": "https://sc.panda321.com/static/base/images/favicon.ico",
		"_hidden": false,
		"_urlTemplate": "https://sc.panda321.com/scholar?hl=zh-CN&as_sdt=0%2C5&q={z:title}",
		"_urlParams": [],
		"_urlNamespaces": {
			"rft": "info:ofi/fmt:kev:mtx:journal",
			"z": "http://www.zotero.org/namespaces/openSearch#",
			"": "http://a9.com/-/spec/opensearch/1.1/"
		},
		"_iconSourceURI": "https://sc.panda321.com/static/base/images/favicon.ico"
	},
	{
		"_name": "CNKI新版",
		"_alias": "CNKI",
		"_description": "CNKI新版",
		"_icon": "http://kns8.cnki.net/favicon.ico",
		"_hidden": false,
		"_urlTemplate": "http://kns8.cnki.net/kns/DefaultResult/Index?dbcode=SCDB&kw={z:title}&korder=SU",
		"_urlParams": [],
		"_urlNamespaces": {
			"z": "http://www.zotero.org/namespaces/openSearch#",
			"": "http://a9.com/-/spec/opensearch/1.1/"
		},
		"_iconSourceURI": "http://kns8.cnki.net/favicon.ico"
	},
	{
		"_name": "南京师范大学图书馆",
		"_alias": "南京师范大学图书馆",
		"_description": "南京师范大学图书馆",
		"_icon": "http://lib.njnu.edu.cn/images/njnulogo.png",
		"_hidden": false,
		"_urlTemplate": "http://opac.njnu.edu.cn/opac/openlink.php?strSearchType=title&match_flag=forward&historyCount=1&strText={z:title}&doctype=ALL&with_ebook=on&displaypg=20&showmode=list&sort=CATA_DATE&orderby=desc&location=ALL&csrf_token=%29lW1vOCx%7B%2F",
		"_urlParams": [],
		"_urlNamespaces": {
			"z": "http://www.zotero.org/namespaces/openSearch#"
		},
		"_iconSourceURI": "http://lib.njnu.edu.cn/images/njnulogo.png"
	},
	{
		"_name": "豆瓣读书",
		"_alias": "豆瓣读书",
		"_description": "豆瓣读书",
		"_icon": "https://book.douban.com/favicon.ico",
		"_hidden": false,
		"_urlTemplate": "https://search.douban.com/book/subject_search?search_text={z:title}&cat=1001",
		"_urlParams": [],
		"_urlNamespaces": {
			"z": "http://www.zotero.org/namespaces/openSearch#"
		},
		"_iconSourceURI": "https://book.douban.com/favicon.ico"
	},
	{
		"_name": "国学数典",
		"_alias": "国学数典",
		"_description": "国学数典",
		"_icon": "https://bbs.ugxsd.com/static/image/common/logo_gxsd.png",
		"_hidden": false,
		"_urlTemplate": "https://bbs.ugxsd.com/search.php?mod=forum&searchid=2634&orderby=lastpost&ascdesc=desc&searchsubmit=yes&kw={z:title}",
		"_urlParams": [],
		"_urlNamespaces": {
			"z": "http://www.zotero.org/namespaces/openSearch#"
		},
		"_iconSourceURI": "https://bbs.ugxsd.com/static/image/common/logo_gxsd.png"
	},
	{
		"_name": "读秀图书",
		"_alias": "读秀图书",
		"_description": "读秀图书",
		"_icon": "https://book.duxiu.com/images/small0408.jpg",
		"_hidden": false,
		"_urlTemplate": "https://book.duxiu.com/search?Field=all&channel=search&sw={z:title}&ecode=utf-8&edtype=&searchtype=&view=0",
		"_urlParams": [],
		"_urlNamespaces": {
			"z": "http://www.zotero.org/namespaces/openSearch#"
		},
		"_iconSourceURI": "https://book.duxiu.com/images/small0408.jpg"
	},
	{
		"_name": "Obsidian",
		"_alias": "Obsidian",
		"_description": "在Obsidian中搜索",
		"_icon": "https://obsidian.md/favicon.ico",
		"_hidden": false,
		"_urlTemplate": "obsidian://search?vault=Zotero&query={z:title}",
		"_urlParams": [],
		"_urlNamespaces": {
			"z": "http://www.zotero.org/namespaces/openSearch#"
		},
		"_iconSourceURI": "https://obsidian.md/favicon.ico"
	},
	{
		"_name": "Open Notes",
		"_alias": "Open Notes",
		"_description": "笔记路径放在Rights字段",
		"_icon": "https://figurebed-iseex.oss-cn-hangzhou.aliyuncs.com/img/20201017133213.png",
		"_hidden": false,
		"_urlTemplate": "file:///{z:rights}",
		"_urlParams": [],
		"_urlNamespaces": {
			"z": "http://www.zotero.org/namespaces/openSearch#",
			"": "http://a9.com/-/spec/opensearch/1.1/"
		},
		"_iconSourceURI": "https://figurebed-iseex.oss-cn-hangzhou.aliyuncs.com/img/20201017133213.png"
	},
	{
		"_name": "TOC of Notes",
		"_alias": "TOC of Notes",
		"_description": "打开所有笔记的目录",
		"_icon": "https://figurebed-iseex.oss-cn-hangzhou.aliyuncs.com/img/20201025110921.png",
		"_hidden": false,
		"_urlTemplate": "file:////Users/a40781/Zotero/Obsidian",
		"_urlParams": [],
		"_urlNamespaces": {
			"z": "http://www.zotero.org/namespaces/openSearch#",
			"": "http://a9.com/-/spec/opensearch/1.1/"
		},
		"_iconSourceURI": "https://figurebed-iseex.oss-cn-hangzhou.aliyuncs.com/img/20201025110921.png"
	},
	{
		"_name": "N-Connected Papers",
		"_alias": "Connected Papers文献网络",
		"_description": "Connected Papers文献网络",
		"_icon": "https://www.connectedpapers.com/favicon.ico",
		"_hidden": false,
		"_urlTemplate": "https://www.connectedpapers.com/search?q={z:title}+{z:year}",
		"_urlParams": [],
		"_urlNamespaces": {
			"rft": "info:ofi/fmt:kev:mtx:journal",
			"z": "http://www.zotero.org/namespaces/openSearch#",
			"": "http://a9.com/-/spec/opensearch/1.1/"
		},
		"_iconSourceURI": "https://www.connectedpapers.com/favicon.ico"
	},
	{
		"_name": "CrossRef",
		"_alias": "CrossRef",
		"_description": "CrossRef Search",
		"_icon": "https://www.crossref.org/favicon.ico",
		"_hidden": false,
		"_urlTemplate": "http://crossref.org/openurl?{z:openURL}&pid=zter:zter321",
		"_urlParams": [],
		"_urlNamespaces": {
			"z": "http://www.zotero.org/namespaces/openSearch#",
			"": "http://a9.com/-/spec/opensearch/1.1/"
		},
		"_iconSourceURI": "http://crossref.org/favicon.ico"
	},
	{
		"_name": "谷歌学术",
		"_alias": "Google Scholar",
		"_description": "Google Scholar Search",
		"_icon": "https://figurebed-iseex.oss-cn-hangzhou.aliyuncs.com/img/20201016230633.png",
		"_hidden": false,
		"_urlTemplate": "http://scholar.google.com/scholar?as_q=&as_epq={z:title}&as_occt=title&as_sauthors={rft:aufirst?}+{rft:aulast?}&as_ylo={z:year?}&as_yhi={z:year?}&as_sdt=1.&as_sdtp=on&as_sdtf=&as_sdts=22&",
		"_urlParams": [],
		"_urlNamespaces": {
			"rft": "info:ofi/fmt:kev:mtx:journal",
			"z": "http://www.zotero.org/namespaces/openSearch#",
			"": "http://a9.com/-/spec/opensearch/1.1/"
		},
		"_iconSourceURI": "https://figurebed-iseex.oss-cn-hangzhou.aliyuncs.com/img/20201016230633.png"
	},
	{
		"_name": "谷歌学术 - Title Only",
		"_alias": "Google Scholar",
		"_description": "Google Scholar Search - Title Only",
		"_icon": "https://figurebed-iseex.oss-cn-hangzhou.aliyuncs.com/img/20201016230633.png",
		"_hidden": false,
		"_urlTemplate": "http://scholar.google.com/scholar?as_q=&as_epq={z:title}&as_occt=title&as_sdt=1.&as_sdtp=on&as_sdtf=&as_sdts=22&",
		"_urlParams": [],
		"_urlNamespaces": {
			"rft": "info:ofi/fmt:kev:mtx:journal",
			"z": "http://www.zotero.org/namespaces/openSearch#",
			"": "http://a9.com/-/spec/opensearch/1.1/"
		},
		"_iconSourceURI": "https://figurebed-iseex.oss-cn-hangzhou.aliyuncs.com/img/20201016230633.png"
	},
	{
		"_name": "谷歌专利",
		"_alias": "Google Scholar",
		"_description": "Google Patent - Search",
		"_icon": "https://figurebed-iseex.oss-cn-hangzhou.aliyuncs.com/img/20201017210030.png",
		"_hidden": false,
		"_urlTemplate": "https://patents.google.com/?q=({z:title})&oq=({z:title})",
		"_urlParams": [],
		"_urlNamespaces": {
			"rft": "info:ofi/fmt:kev:mtx:journal",
			"z": "http://www.zotero.org/namespaces/openSearch#",
			"": "http://a9.com/-/spec/opensearch/1.1/"
		},
		"_iconSourceURI": "https://figurebed-iseex.oss-cn-hangzhou.aliyuncs.com/img/20201017210030.png"
	},
	{
		"_name": "Semantic Scholar - DOI",
		"_alias": "Semantic Scholar",
		"_description": "Semantic Scholar",
		"_icon": "https://figurebed-iseex.oss-cn-hangzhou.aliyuncs.com/img/20201017165044.png",
		"_hidden": false,
		"_urlTemplate": "https://api.semanticscholar.org/{z:DOI}",
		"_urlParams": [],
		"_urlNamespaces": {
			"rft": "info:ofi/fmt:kev:mtx:journal",
			"z": "http://www.zotero.org/namespaces/openSearch#",
			"": "http://a9.com/-/spec/opensearch/1.1/"
		},
		"_iconSourceURI": "https://figurebed-iseex.oss-cn-hangzhou.aliyuncs.com/img/20201017165044.png"
	},
	{
		"_name": "Google",
		"_alias": "Google",
		"_description": "Google Search",
		"_icon": "https://figurebed-iseex.oss-cn-hangzhou.aliyuncs.com/img/20201016230909.png",
		"_hidden": false,
		"_urlTemplate": "https://www.google.com/#q={z:title}+{rft:aufirst?}+{rft:aulast?}",
		"_urlParams": [],
		"_urlNamespaces": {
			"z": "http://www.zotero.org/namespaces/openSearch#"
		},
		"_iconSourceURI": "https://figurebed-iseex.oss-cn-hangzhou.aliyuncs.com/img/20201016230909.png"
	},
	{
		"_name": "Web of Science",
		"_alias": "WOS",
		"_description": "Web of Science Search",
		"_icon": "https://figurebed-iseex.oss-cn-hangzhou.aliyuncs.com/img/20201016231207.png",
		"_hidden": false,
		"_urlTemplate": "http://ws.isiknowledge.com/cps/openurl/service?url_ver=Z39.88-2004&{z:openURL}",
		"_urlParams": [],
		"_urlNamespaces": {
			"rft": "info:ofi/fmt:kev:mtx:journal",
			"z": "http://www.zotero.org/namespaces/openSearch#"
		},
		"_iconSourceURI": "https://figurebed-iseex.oss-cn-hangzhou.aliyuncs.com/img/20201016231207.png"
	},
	{
		"_name": "WOS Citing Articles",
		"_alias": "WOS Citing Articles",
		"_description": "Web of Science Citing Articles Search",
		"_icon": "https://figurebed-iseex.oss-cn-hangzhou.aliyuncs.com/img/20201016231207.png",
		"_hidden": false,
		"_urlTemplate": "http://ws.isiknowledge.com/cps/openurl/service?url_ver=Z39.88-2004&svc_val_fmt=info:ofi/fmt:kev:mtx:sch_svc&svc.citing=yes&{z:openURL}",
		"_urlParams": [],
		"_urlNamespaces": {
			"rft": "info:ofi/fmt:kev:mtx:journal",
			"z": "http://www.zotero.org/namespaces/openSearch#"
		},
		"_iconSourceURI": "https://figurebed-iseex.oss-cn-hangzhou.aliyuncs.com/img/20201016231207.png"
	},
	{
		"_name": "WOS Related Articles",
		"_alias": "WOS Related Articles",
		"_description": "Web of Science Related Articles Search",
		"_icon": "https://figurebed-iseex.oss-cn-hangzhou.aliyuncs.com/img/20201016231207.png",
		"_hidden": false,
		"_urlTemplate": "http://ws.isiknowledge.com/cps/openurl/service?url_ver=Z39.88-2004&svc_val_fmt=info:ofi/fmt:kev:mtx:sch_svc&svc.related=yes&{z:openURL}",
		"_urlParams": [],
		"_urlNamespaces": {
			"rft": "info:ofi/fmt:kev:mtx:journal",
			"z": "http://www.zotero.org/namespaces/openSearch#"
		},
		"_iconSourceURI": "https://figurebed-iseex.oss-cn-hangzhou.aliyuncs.com/img/20201016231207.png"
	},
	{
		"_name": "Sci-Hub DOI",
		"_alias": "Sci-Hub DOI",
		"_description": "SciHub Lookup Lookup",
		"_icon": "https://figurebed-iseex.oss-cn-hangzhou.aliyuncs.com/img/20201016200912.png",
		"_hidden": false,
		"_urlTemplate": "http://sci-hub.shop/{z:DOI}",
		"_urlParams": [],
		"_urlNamespaces": {
			"z": "http://www.zotero.org/namespaces/openSearch#"
		},
		"_iconSourceURI": "https://figurebed-iseex.oss-cn-hangzhou.aliyuncs.com/img/20201016200912.png"
	},
	{
		"_name": "Sci-Hub URL",
		"_alias": "Sci-Hub URL",
		"_description": "SciHub URL Lookup",
		"_icon": "https://figurebed-iseex.oss-cn-hangzhou.aliyuncs.com/img/20201016200912.png",
		"_hidden": false,
		"_urlTemplate": "http://sci-hub.shop/{z:url}",
		"_urlParams": [],
		"_urlNamespaces": {
			"z": "http://www.zotero.org/namespaces/openSearch#"
		},
		"_iconSourceURI": "https://figurebed-iseex.oss-cn-hangzhou.aliyuncs.com/img/20201016200912.png"
	},
	{
		"_name": "Sci-Hub最新网址",
		"_alias": "Sci-Hub最新网址",
		"_description": "Sci-Hub最新网址",
		"_icon": "https://figurebed-iseex.oss-cn-hangzhou.aliyuncs.com/img/20201016200912.png",
		"_hidden": false,
		"_urlTemplate": "https://iseex.github.io/scihub/",
		"_urlParams": [],
		"_urlNamespaces": {
			"z": "http://www.zotero.org/namespaces/openSearch#",
			"": "http://a9.com/-/spec/opensearch/1.1/"
		},
		"_iconSourceURI": "https://figurebed-iseex.oss-cn-hangzhou.aliyuncs.com/img/20201016200912.png"
	},
	{
		"_name": "Connected Papers（手动输入doi）",
		"_alias": "Connected Papers文献网络",
		"_description": "Connected Papers文献网络",
		"_icon": "https://www.connectedpapers.com/favicon.ico",
		"_hidden": false,
		"_urlTemplate": "https://www.connectedpapers.com",
		"_urlParams": [],
		"_urlNamespaces": {
			"rft": "info:ofi/fmt:kev:mtx:journal",
			"z": "http://www.zotero.org/namespaces/openSearch#",
			"": "http://a9.com/-/spec/opensearch/1.1/"
		},
		"_iconSourceURI": "https://www.connectedpapers.com/favicon.ico"
	},
	{
		"_name": "Connected Papers（Title Only）",
		"_alias": "Connected Papers文献网络",
		"_description": "Connected Papers文献网络",
		"_icon": "https://www.connectedpapers.com/favicon.ico",
		"_hidden": false,
		"_urlTemplate": "https://www.connectedpapers.com/search?q={z:title}",
		"_urlParams": [],
		"_urlNamespaces": {
			"rft": "info:ofi/fmt:kev:mtx:journal",
			"z": "http://www.zotero.org/namespaces/openSearch#",
			"": "http://a9.com/-/spec/opensearch/1.1/"
		},
		"_iconSourceURI": "https://www.connectedpapers.com/favicon.ico"
	},
	{
		"_name": "iJournal期刊影响因子（首选1）",
		"_alias": "iJournal期刊影响因子",
		"_description": "期刊影响因子查询（仅支持搜索ISSN）",
		"_icon": "https://ijournal.topeditsci.com/favicon.ico",
		"_hidden": false,
		"_urlTemplate": "https://ijournal.topeditsci.com/search?keywordType=title&keyword={rft:jtitle}&ifStart2019=&ifEnd2019=&jcr=&sub=&isDomestic=&selfCitingRate=all&compatriotRate=all&totalReviewRatio=all&categoryId=&pageNum=1&order=&orderType=",
		"_urlParams": [],
		"_urlNamespaces": {
			"rft": "info:ofi/fmt:kev:mtx:journal",
			"z": "http://www.zotero.org/namespaces/openSearch#",
			"": "http://a9.com/-/spec/opensearch/1.1/"
		},
		"_iconSourceURI": "https://ijournal.topeditsci.com/favicon.ico"
	},
	{
		"_name": "JustScience影响因子（首选2）",
		"_alias": "JustScience期刊影响因子（首选2）",
		"_description": "JustScience期刊影响因子（首选2）",
		"_icon": "https://figurebed-iseex.oss-cn-hangzhou.aliyuncs.com/img/20201017105103.png",
		"_hidden": false,
		"_urlTemplate": "https://sci.justscience.cn/index.php?q={rft:jtitle}&sci=1",
		"_urlParams": [],
		"_urlNamespaces": {
			"rft": "info:ofi/fmt:kev:mtx:journal",
			"z": "http://www.zotero.org/namespaces/openSearch#",
			"": "http://a9.com/-/spec/opensearch/1.1/"
		},
		"_iconSourceURI": "https://figurebed-iseex.oss-cn-hangzhou.aliyuncs.com/img/20201017105103.png"
	},
	{
		"_name": "中文期刊搜索",
		"_alias": "中文期刊搜索",
		"_description": "JustScience中文期刊搜索",
		"_icon": "https://figurebed-iseex.oss-cn-hangzhou.aliyuncs.com/img/20201017105103.png",
		"_hidden": false,
		"_urlTemplate": "https://sci.justscience.cn/index.php?q={rft:jtitle}&sci=0",
		"_urlParams": [],
		"_urlNamespaces": {
			"rft": "info:ofi/fmt:kev:mtx:journal",
			"z": "http://www.zotero.org/namespaces/openSearch#",
			"": "http://a9.com/-/spec/opensearch/1.1/"
		},
		"_iconSourceURI": "https://figurebed-iseex.oss-cn-hangzhou.aliyuncs.com/img/20201017105103.png"
	},
	{
		"_name": "Letpub期刊搜索",
		"_alias": "Letpub期刊搜索",
		"_description": "Letpub期刊搜索（仅支持搜索ISSN）",
		"_icon": "https://www.letpub.com.cn/favicon.ico",
		"_hidden": false,
		"_urlTemplate": "http://www.letpub.com.cn/index.php?page=journalapp&view=search&searchname={rft:jtitle}",
		"_urlParams": [],
		"_urlNamespaces": {
			"rft": "info:ofi/fmt:kev:mtx:journal",
			"z": "http://www.zotero.org/namespaces/openSearch#",
			"": "http://a9.com/-/spec/opensearch/1.1/"
		},
		"_iconSourceURI": "https://www.letpub.com.cn/favicon.ico"
	},
	{
		"_name": "期刊影响因子查询",
		"_alias": "期刊影响因子查询",
		"_description": "期刊影响因子查询（仅支持搜索ISSN）",
		"_icon": "https://www.xueky.com/favicon.ico",
		"_hidden": false,
		"_urlTemplate": "https://www.xueky.com/rank.php?qk={rft:jtitle}",
		"_urlParams": [],
		"_urlNamespaces": {
			"rft": "info:ofi/fmt:kev:mtx:journal",
			"z": "http://www.zotero.org/namespaces/openSearch#",
			"": "http://a9.com/-/spec/opensearch/1.1/"
		},
		"_iconSourceURI": "https://www.xueky.com/favicon.ico"
	},
	{
		"_name": "期刊近五年影响因子",
		"_alias": "期刊近五年影响因子",
		"_description": "期刊近五年影响因子",
		"_icon": "https://figurebed-iseex.oss-cn-hangzhou.aliyuncs.com/img/20201016200307.png",
		"_hidden": false,
		"_urlTemplate": "http://www.greensci.net/search?kw={rft:jtitle}",
		"_urlParams": [],
		"_urlNamespaces": {
			"rft": "info:ofi/fmt:kev:mtx:journal",
			"z": "http://www.zotero.org/namespaces/openSearch#",
			"": "http://a9.com/-/spec/opensearch/1.1/"
		},
		"_iconSourceURI": "https://figurebed-iseex.oss-cn-hangzhou.aliyuncs.com/img/20201016200307.png"
	},
	{
		"_name": "Unpaywall",
		"_alias": "Unpaywall",
		"_description": "Unpaywall Lookup",
		"_icon": "https://oadoi.org/static/img/favicon.png",
		"_hidden": false,
		"_urlTemplate": "https://oadoi.org/{z:DOI}",
		"_urlParams": [],
		"_urlNamespaces": {
			"z": "http://www.zotero.org/namespaces/openSearch#"
		},
		"_iconSourceURI": "https://oadoi.org/static/img/favicon.png"
	},
	{
		"_name": "LibGen",
		"_alias": "LibGen",
		"_description": "Look up books on Library Genesis",
		"_icon": "http://gen.lib.rus.ec/favicon.ico",
		"_hidden": false,
		"_urlTemplate": "http://gen.lib.rus.ec/search.php?req={rft:aufirst?}+{rft:aulast?}+{rft:title?}+{z:ISBN?}",
		"_urlParams": [],
		"_method": "GET",
		"_urlNamespaces": {
			"rft": "info:ofi/fmt:kev:mtx:book",
			"xmlns": "http://a9.com/-/spec/opensearch/1.1/",
			"z": "http://www.zotero.org/namespaces/openSearch#"
		},
		"_iconSourceURI": "http://gen.lib.rus.ec/favicon.ico"
	},
	{
		"_name": "Wikipedia",
		"_alias": "Wikipedia",
		"_description": "Wikipedia",
		"_icon": "https://figurebed-iseex.oss-cn-hangzhou.aliyuncs.com/img/20201016232045.png",
		"_hidden": false,
		"_urlTemplate": "https://zh.wikipedia.org/wiki/{z:title}",
		"_urlParams": [],
		"_urlNamespaces": {
			"z": "http://www.zotero.org/namespaces/openSearch#",
			"": "http://a9.com/-/spec/opensearch/1.1/"
		},
		"_iconSourceURI": "https://figurebed-iseex.oss-cn-hangzhou.aliyuncs.com/img/20201016232045.png"
	},
	{
		"_name": "ProQuest",
		"_alias": "ProQuest",
		"_description": "ProQuest Search",
		"_icon": "https://www.proquest.com/favicon.ico",
		"_hidden": false,
		"_urlTemplate": "http://proquest.umi.com/pqdweb?SQ=TI(+{z:title}+)+YR(+{z:year?}+)&RQT=305&querySyntax=PQ&searchInterface=1&moreOptState=CLOSED&TS=1139706667&JSEnabled=1&DBId=-1",
		"_urlParams": [],
		"_urlNamespaces": {
			"rft": "info:ofi/fmt:kev:mtx:journal",
			"z": "http://www.zotero.org/namespaces/openSearch#"
		},
		"_iconSourceURI": "http://www.proquest.com/favicon.ico"
	},
	{
		"_name": "Zlibrary Book",
		"_alias": "Zlibrary Book",
		"_description": "Zlibrary Book",
		"_icon": "https://z-lib.org/favicon.ico",
		"_hidden": false,
		"_urlTemplate": "https://b-ok.cc/s/{z:title}",
		"_urlParams": [],
		"_urlNamespaces": {
			"z": "http://www.zotero.org/namespaces/openSearch#",
			"": "http://a9.com/-/spec/opensearch/1.1/"
		},
		"_iconSourceURI": "https://z-lib.org/favicon.ico"
	},
	{
		"_name": "Zlibrary Articles",
		"_alias": "Zlibrary Articles",
		"_description": "Zlibrary Articles",
		"_icon": "https://z-lib.org/favicon.ico",
		"_hidden": false,
		"_urlTemplate": "https://booksc.xyz/s/{z:title}",
		"_urlParams": [],
		"_urlNamespaces": {
			"z": "http://www.zotero.org/namespaces/openSearch#",
			"": "http://a9.com/-/spec/opensearch/1.1/"
		},
		"_iconSourceURI": "https://z-lib.org/favicon.ico"
	},
	{
		"_name": "SooPAT专利搜索",
		"_alias": "SooPAT专利搜索",
		"_description": "SooPAT专利搜索",
		"_icon": "http://www.soopat.com/favicon.ico",
		"_hidden": false,
		"_urlTemplate": "http://www.soopat.com/Home/Result?SearchWord={z:title}&FMZL=Y&SYXX=Y&WGZL=Y&FMSQ=Y",
		"_urlParams": [],
		"_urlNamespaces": {
			"z": "http://www.zotero.org/namespaces/openSearch#",
			"": "http://a9.com/-/spec/opensearch/1.1/"
		},
		"_iconSourceURI": "http://www.soopat.com/favicon.ico"
	},
	{
		"_name": "百度学术搜索",
		"_alias": "BaiDu",
		"_description": "百度学术搜索",
		"_icon": "http://xueshu.baidu.com/favicon.ico",
		"_hidden": false,
		"_urlTemplate": "https://xueshu.baidu.com/s?wd={z:title}&rsv_bp=0&tn=SE_baiduxueshu_c1gjeupa&rsv_spt=3&ie=utf-8&f=8&rsv_sug2=0&sc_f_para=sc_tasktype%3D%7BfirstSimpleSearch%7D",
		"_urlParams": [],
		"_urlNamespaces": {
			"z": "http://www.zotero.org/namespaces/openSearch#",
			"": "http://a9.com/-/spec/opensearch/1.1/"
		},
		"_iconSourceURI": "http://xueshu.baidu.com/favicon.ico"
	},
	{
		"_name": "万方搜索",
		"_alias": "万方搜索",
		"_description": "万方搜索",
		"_icon": "http://www.wanfangdata.com.cn/favicon.ico",
		"_hidden": false,
		"_urlTemplate": "http://www.wanfangdata.com.cn/search/searchList.do?searchType=all&showType=&pageSize=&searchWord={z:title}&isTriggerTag=",
		"_urlParams": [],
		"_urlNamespaces": {
			"z": "http://www.zotero.org/namespaces/openSearch#",
			"": "http://a9.com/-/spec/opensearch/1.1/"
		},
		"_iconSourceURI": "http://www.wanfangdata.com.cn/favicon.ico"
	},
	{
		"_name": "谷粉学术",
		"_alias": "谷粉学术",
		"_description": "谷粉学术",
		"_icon": "https://img.99lb.net/favicon.ico",
		"_hidden": false,
		"_urlTemplate": "https://cc.gufenxueshu.com/scholar?q={z:title}",
		"_urlParams": [],
		"_urlNamespaces": {
			"z": "http://www.zotero.org/namespaces/openSearch#",
			"": "http://a9.com/-/spec/opensearch/1.1/"
		},
		"_iconSourceURI": "https://img.99lb.net/favicon.ico"
	},
	{
		"_name": "Glgoo学术",
		"_alias": "Glgoo学术",
		"_description": "Glgoo学术",
		"_icon": "https://xue.glgoo.org/favicon.ico",
		"_hidden": false,
		"_urlTemplate": "https://xue.xiayige.org/scholar?hl=zh-CN&q={z:title}&btnG=&lr=",
		"_urlParams": [],
		"_urlNamespaces": {
			"z": "http://www.zotero.org/namespaces/openSearch#",
			"": "http://a9.com/-/spec/opensearch/1.1/"
		},
		"_iconSourceURI": "https://xue.glgoo.org/favicon.ico"
	}
]
```

#### 更新翻译器
>【注】下方2.0.3、2.0.4内容也可以直接观看这个 up 主的[视频教程]( https://www.bilibili.com/video/BV13d4y1Z78D "视频教程")
{{< bilibili id=BV13d4y1Z78D >}}

1) 将蓝奏云中`translators.zip`解压，将解压后的文件全部复制，粘贴到 zotero 数据文件夹——translators 文件夹中
![image](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311071538689.png)
2) 【Zotero】—【编辑】—【首选项】—【茉莉花】—【非官方维护中文翻译器】，先点`刷新`，再点`更新全部`
![image](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311071539794.png)
3) 打开安装了 Zotero Connector 插件的浏览器，我这里是 edge。打开扩展，将 Zotero Connector 插件设为`在工具栏中显示`
![image](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311071539438.png)
4) 右键单击 Zotero Connector 插件图标——扩展选项——Advanced——勾选图中两项，然后多点几下 update
![image](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311071539986.png)

#### 设置 scihub 下载文献
【Zotero】—【编辑】—【首选项】—— 【高级】—— 【设置编辑器】
![image](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311071539685.png)
搜索`extensions.zotero.findPDFs.resolvers`，双击打开，默认情况下是只有一对`[]`，删除`[]`，并将以下代码粘贴进去。
```json
{
    "name":"Sci-Hub",
    "method":"GET",
    "url":"https://sci-hub.se/{doi}",
    "mode":"html",
    "selector":"#pdf",
    "attribute":"src",
    "automatic":true
}
```

到此就成功将 Sci-Hub 配置为 PDF 解析器了，也就是说替代了默认的 Unpaywall。现在，无需重启 Zotero，即可调用 Sci-Hub 免费下载文献了。
>【注】此处参考自[文章]( https://mp.weixin.qq.com/s/QMSG24tgn4z8ShfE9pVYMg "文章")。

### 常规
我的常规配置：
![image](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311071540110.png)
### 同步
我采用了坚果云进行同步。
![image](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311071540066.png)
#### 坚果云使用
1) 注册【[坚果云]( https://www.jianguoyun.com/ "坚果云")账户】
2) 点击右上角【用户名】—进入【账户信息】
3) 进入【安全选项】
4) 向下拖动进入【第三方应用管理】—点击【添加应用】—输入应用名【zotero】
这里【示例】中的【服务器地址】、【账户】和【密码】（应用密码）即是【WebDAV】需填写的【URL】、【用户名】和【密码】
![image](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311071540455.png)
5) 返回【Zotero】—【首选项】—【同步】 将【同步文献库的附件】改为【WebDAV】，输入【URL】、【用户名】和【密码】，点击【验证服务器】成功即可。
![image](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311071540139.png)

>【注】坚果云验证失败看[这里]( https://mp.weixin.qq.com/s/2QhDmtWu6ISgDZ9FrIdIBw "这里")。

### 引用
#### zotero 官方7714样式
1. 点击【获取更多样式】
2. 搜索【7714】即可安装国标引用样式。注意有1987、2005和2015三个时间，note、author-date 和 numeric 三个格式，鼠标悬停即可【预览】样式。
![image](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311071542774.png)

#### 比较贴近东北大学要求的7714样式
zotero 官方的7714样式存在一些问题，如不能区分中英文文献，导致引用英文文献也是“等”，而不是“et al”。github 上的[Chinese-STD-GB-T-7714-related-csl]( https://github.com/redleafnew/Chinese-STD-GB-T-7714-related-csl "Chinese-STD-GB-T-7714-related-csl")仓库（[Gitee]( https://gitee.com/redleafnew00/Chinese-STD-GB-T-7714-related-csl "Gitee")）提供7714 2015的官方样式及众多修改版，其中[002gb]( https://github.com/redleafnew/Chinese-STD-GB-T-7714-related-csl/blob/main/002gb-t-7714-2015-numeric-bilingual-no-uppercase-no-url-doi.csl "002gb")样式比较符合东北大学的要求，除了网络文献的引用顺序有点差异。
![image](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311071542161.png)

1. 从仓库或者前文的蓝奏云链接中下载样式
2. 点击+号，选中已下载的002 csl 样式，打开。
会提示`***.csl不是一个有效的 CSL 1.0.2 样式文件，你可能不能和Zotero一起正常工作`，不用管，点击 OK 继续导入。
![image](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311071542053.png)
3. 点击 OK 保存退出首选项。然后重新打开【编辑】—【首选项】— 【导出】— 项目格式，选择为7714
![image](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311071542424.png)

## 插件配置
下面这些插件都建议在[中文插件网站](https://plugins.zotero-chinese.com/#/)下载。注意要下载对应 zotero 版本的插件，本文中下载的都是 zotero6的插件。
### Zotero 插件合集
点击工具栏中的 [![image](https://github.com/syt2/zotero-addons/raw/z6/addon/chrome/content/icons/favicon.png)]( https://github.com/syt2/zotero-addons/blob/z6/addon/chrome/content/icons/favicon.png ) ，自动管理、更新、添加 Zotero 插件
![image.png](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311082224234.png)

### ZotFile
#### 功能
- 自动修改附件名
- 提取附件中的笔记
- 【Attaching New Files】—添加新附件
- 【Send to Tablet】—多端同步阅读
#### 配置
点击【工具】—进入【Zotfile 首选项】
- 【General Settings】
  - 【Source Folder For Attaching New Files】：自动抓取新附件建议设置为【浏览器等默认下载地址】
  - 【Location of Files】：附件本地存储地址建议选择【Attach stored copy of files(s)】，存储在 Zotero 的根目录下
	![image](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311071543441.png)
- 【Send to Tablet】：若非本地存储空间不够，不建议使用
具体设置可参考[此处]( https://mp.weixin.qq.com/s/uHOY2a_EZqJAQOrB2v9rFQ "此处")
- 【Renaming Rules】和【Advanced Settings】：可自行修改
![image](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311071543092.png)

### [ZoteroQuickLook]( https://github.com/404neko/ZoteroQuickLookReload "ZoteroQuickLook")
#### 功能
按【空格】实现快速预览
#### 配置
1. 下载【QuickLook】本体安装，记住安装目录
Windows：[QuickLook for Windows]( https://github.com/QL-Win/QuickLook/releases "QuickLook for Windows")
2. 【Zotero】—【编辑】—【首选项】—— 【高级】—— 【设置编辑器】，搜索`extensions.zoteroquicklook.customviewcommand`，双击将里面的内容修改为`QuickLook.exe`的文件路径
![image](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311071543870.png)

### [茉莉花-Jasminum]( https://github.com/l0o0/jasminum "茉莉花-Jasminum")
#### 功能
- 拆分或合并 Zotero 中条目作者姓和名
- 根据知网上下载的文献文件来抓取引用信息（根据文件名）
- 添加中文 PDF/CAJ 时，自动拉取知网数据，该功能默认关闭。需要到设置中开启，注意添加的文件名需要含有中文，全英文没有效果（根据文件名）
- 为知网的学位论文 PDF 添加书签
- 更新中文翻译器

#### 配置
如何自动为知网学位论文添加【书签】
从知网下载的 PDF 格式【学位论文】不显示书签（CAJ 格式显示），【茉莉花】提供自动添加功能。要使用添加【书签】功能需要下载【PDFtk Server】，文件见网盘。

下载并安装【PDFtk Server】，蓝奏云里有
打开【Zotero】—进入【首选项】—进入【茉莉花】 选择【PDFtk Server】的路径，最后须选择 bin
![image](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311071543556.png)

### zotero citation update
#### 功能
更新文献被引用数
#### 配置
列标题启用【存档位置】
![image](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311071543229.png)

使用：工具——更新引用
![image](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311071544321.png)
### Zotero PDF Translate
- 各翻译引擎 api 格式设置详见[github]( https://github.com/windingwind/zotero-pdf-translate#readme "github")
- 各翻译引擎 api[中文申请教程]( https://doc.tern.1c7.me/zh/folder/setting/#%E5%B0%8F%E7%89%9B "中文申请教程")
>【注】不想看文字的也可以看这个 up 的[视频讲解]( https://www.bilibili.com/video/BV1q94y1D7dy "视频讲解")，演示了如何申请小牛 api
{{< bilibili id=BV1q94y1D7dy >}}
#### 使用与功能
双击 PDF 附件（要用 zotero 打开 PDF）。点击右上角展开翻译窗口。鼠标选中文字自动翻译。
![image](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311071544208.png)

#### 翻译引擎配置
建议使用腾讯云 api，免费额度量大管饱，翻译效果也很好。或者小牛、有道智云，这两虽然免费额度是有期限的，但是可以建立自己的术语表，翻译起来更准确。
>【注】小牛翻译注册后需要在首页手动领取100万免费流量，有效期一年
![image](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311071544542.png)

### [Crush Reference](https://github.com/MuiseDestiny/zotero-reference)
论文右侧——参考文献——点击“刷新”，自动拉取参考文献目录。
![image.png](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311082216865.png)
### 移动端 ：多平台同步阅读环境配置
具体操作与 [#2.2 同步](#同步) 设置相同
- iPadOS：【Papership【绑定 Zotero 账号+WebDav
可参考 [青柠学术 - 详解【Zotero+PaperShip+坚果云】文献生态的同步机制！]( https://mp.weixin.qq.com/s?__biz=MzAxNzgyMDg0MQ==&mid=2650456887&idx=2&sn=f33a0a4461ee915e1c8f9880066cab68&chksm=83d1def1b4a657e7d9d7c18062dbb1977725e9a891294b686379311d71d9fcf1beac81e168bb&scene=178&cur_album_id=1319074508795641857#rd "青柠学术 - 详解【Zotero+PaperShip+坚果云】文献生态的同步机制！")
- Android：【Zoo for Zotero】绑定 Zotero 账号+WebDav
可参考 [青柠学术 - Zoo for Zotero，安卓上阅读 Zotero 文献的利器！]( https://mp.weixin.qq.com/s?__biz=MzAxNzgyMDg0MQ==&mid=2650456795&idx=2&sn=2060a39b9ed6798c1990aa72765c637e&chksm=83d1df1db4a6560b76ee330c13a917027b271ce9e61bb8aad31cf28bbbb0e95459763b67af63&scene=178&cur_album_id=1319074508795641857#rd "青柠学术 - Zoo for Zotero，安卓上阅读 Zotero 文献的利器！")

## 工作流
### 联动 obsidian
参考[最新zotero与obsidian笔记联动教程（可代替citations和mdnotes）](https://blog.csdn.net/qq_43309940/article/details/125150487)

### 工作流：以 Zotero 为中枢
还是参考 Eleven 的[知乎专栏]( https://zhuanlan.zhihu.com/p/347493385 "知乎专栏")

![image](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311071545111.png)
- 检索 / 阅读 / 笔记
	- 确定题目 / 开题报告 / 文献综述
		- 下载论文——Zotero 抓取
		- 可视化文献处理——Zotero 存储 bib，导出处理
		- 多端同步阅读——移动端同步 Zotero 账号
	- 存档 & 归类——Zotero 文件夹分类以及 Tag 分类
	- 文献笔记——与 Zotero 条目联结
- 写作
	- 插入引文生成参考文献——Zotero 通过文字处理软件插件插入参考文献
	- 调整格式——修改 Zotero 参考文献引用格式设置
- 回溯
	- 用 Zotero 搭建自己的知识库

### 下载论文
- 正着下：抓取
	- 单篇——浏览器中打开一篇论文的详情页，左键点击右上角【插件】，出现【Full Text PDF】即为成功
![image](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311071545565.png)

	- 批量——在知网搜索页面点击右上角【插件】，跳出【Zotero Item Selector】
![image](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311071545250.png)

- 反着下
	- 识别：从文献到题录
英文文献会自动抓取元数据，若失败请点【重新抓取 PDF 的元数据】
![image](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311071545378.png)

	- 检索：从题录到文献，利用【搜索引擎】进入知网下载文献
![image](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311071545208.png)

### 储存&分类
#### 新建分类
![image](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311071546648.png)
#### Tag 管理
- 添加 Tag
![image](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311071546235.png)

- 给 Tag 添加颜色
![image](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311071546746.png)

- 检索 Tag：单击左下角【Tag 区】中的 Tag

#### 高级检索
![image](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311071546029.png)

### 阅读
#### 导出 PDF 批注
![image](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311071546337.png)

#### 联结文献笔记

### 写作
#### 插入参考文献
![image](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311071547790.png)
### 分享
#### 导出条目及附件
导出分类，然后选择【Zotero RDF】格式，勾选附件和笔记
![image](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311071547804.png)

#### 团队协作
- 新建群组
![image](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311071547803.png)
- 三种类型的群组
![image](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311071547093.png)


---

> 作者: [云吱](https://haoyep.com/)  
> URL: https://haoyep.com/posts/zotero-config/  


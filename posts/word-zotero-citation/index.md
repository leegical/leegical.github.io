# 在 Word 中使用 Zotero 插入参考文献

本文介绍了如何在 Word 中使用 Zotero 插入参考文献，并设定东北大学要求的参考文献引用列表格式。

&lt;!--more--&gt;

## 准备工作
### 参考文献引用格式
安装 GB/T 7714-2015 参考文献引用格式。
#### Zotero 官方7714样式（不推荐）
{{&lt; admonition &gt;}}
此官方格式存在一些问题，如不能区分中英文文献，导致引用英文文献也是“等”，而不是“et al”。因此并不推荐。
{{&lt; /admonition &gt;}}

1. 打开 Zotero，点击`编辑`-&gt;`首选项`-&gt;`引用`
2. 在`样式`中点击`获取更多样式`
3. 搜索`7714`即可安装国标引用样式。注意有1987、2005和2015三个时间，note、author-date 和 numeric 三个格式，鼠标悬停即可预览样式
![安装Zotero 官方7714样式](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311071542774.png)
#### 比较贴近 NEU 要求的7714样式
Github 上的[Chinese-STD-GB-T-7714-related-csl]( https://github.com/redleafnew/Chinese-STD-GB-T-7714-related-csl &#34;Chinese-STD-GB-T-7714-related-csl&#34;)仓库（或[Gitee 镜像仓库]( https://gitee.com/redleafnew00/Chinese-STD-GB-T-7714-related-csl &#34;Gitee&#34;)）提供7714 2015的官方样式及众多修改版，其中[002gb]( https://github.com/redleafnew/Chinese-STD-GB-T-7714-related-csl/blob/main/002gb-t-7714-2015-numeric-bilingual-no-uppercase-no-url-doi.csl &#34;002gb&#34;)样式比较符合东北大学的要求，除了网络文献的引用顺序有点差异。
![002gb样式](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311071542161.png)

1. 点击 \[[Github](https://raw.githubusercontent.com/redleafnew/Chinese-STD-GB-T-7714-related-csl/main/002gb-t-7714-2015-numeric-bilingual-no-uppercase-no-url-doi.csl) | [Gitee](https://gitee.com/redleafnew00/Chinese-STD-GB-T-7714-related-csl/raw/main/002gb-t-7714-2015-numeric-bilingual-no-uppercase-no-url-doi.csl) \]下载引用格式文件
2. 打开 Zotero，依次进入`编辑`-&gt;`首选项`-&gt;`引用`
3. 点击`&#43;`号添加样式。选中已下载的002 csl 样式，打开。
![导入样式](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311071542053.png)
&gt;会提示`***.csl不是一个有效的 CSL 1.0.2 样式文件，你可能不能和Zotero一起正常工作`，不用管，点击 OK 继续导入。
![不管提示，继续导入](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202404011457740.png)

4. 点击 OK 保存退出首选项。然后重新打开`编辑`-&gt;`首选项`-&gt;`导出`—&gt;**条目格式**，设置成刚才导入的7714样式
![设置默认导出样式](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202404011502945.png)
### 在 Word 中安装 Zotero 插件
1. 关闭所有已经打开的 Word
2. 打开 Zotero，点击`编辑`-&gt;`首选项`-&gt;`引用`
3. 在`文档编辑软件`中点击`安装加载项 Microsoft Word`，记得勾选`使用经典版&#34;添加引注&#34;`
![安装加载项 Microsoft Word](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202404011508777.png)

## Zotero Word 插件选项卡
![Zotero Word 插件选项卡](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202404011513060.png)

一般情况下，Zotero 安装时会安装 Zotero Word 插件，其会在 Microsoft Word 里添加一个 Zotero 选项卡。如果你的 Word 里没有 Zotero 选项卡，请参见 [故障排除 | 安装 Zotero 的 Word 插件](https://zotero-chinese.com/user-guide/faqs/word-addon.html#%E6%B3%A8%E6%84%8F%E4%BA%8B%E9%A1%B9%E5%8F%8A%E4%B8%8E%E6%A0%B7%E5%BC%8F%E7%9B%B8%E5%85%B3%E7%9A%84%E5%B8%B8%E8%A7%81%E9%97%AE%E9%A2%98) 。

Zotero 选项卡包含以下图标：

| 名称         | 图标                                                                                 | 描述                                                                              |
| ---------- | ---------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- |
| 添加/编辑引注    | ![插入引文](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202404011515777.png)    | 在光标位置添加新引注或编辑文档中的现有引注。                                                          |
| 添加/编辑参考文献表 | ![添加参考文献表](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202404011517521.png) | 在光标位置插入参考文献表或编辑现有书目。                                                            |
| 添加笔记       | ![添加笔记](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202404011518001.png)    | 在光标当前位置插入笔记。请注意，此功能不常用，点击后会出现黄色插入框。如果不小心点开了，可以用键盘上的 `Esc` 键关闭黄色插入框。             |
| 文档首选项      | ![文档首选项](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202404011518149.png)   | 打开“文档首选项”窗口，例如更改引文样式。                                                           |
| 刷新         | ![刷新](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202404011518120.png)      | 立即刷新所有引注和参考文献表，更新 Zotero 库中已更改的项目元数据。                                           |
| 取消链接引注     | ![unlink](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202404011519095.png)  | 通过删除域代码来取消文档中 Zotero 引文的链接。这可以防止引文和书目的任何进一步自动更新。请注意，删除域代码是不可逆的，通常只能在文档的最终副本中完成。 |

其中，**文档首选项**窗口允许您设置以下针对该文档的设置：
1. **引文样式**：一般情况下，你只需要修改这一项，其余设置均保持默认即可。    
2. 设置引注和参考文献表的格式的语言。    
3. 对于基于注释的样式，例如“China National Standard GB/T 7714-2015（note，Chinese）”，引文是插入为脚注还或尾注。脚注和尾注的样式和格式由 Word（而不是 Zotero）控制。    
4. 将引文存储为字段还是书签。默认为“字段”。除非您需要使用 LibreOffice 与同事协作，否则应始终选择“字段”。    
5. 对于缩写期刊标题的样式（例如，“Nature”），是否使用 MEDLINE 缩写列表来缩写标题。如果选择此选项（默认值），则 Zotero 中“ ”字段的内容将被忽略。    
6. **是否自动更新引注和参考文献表**：一般情况下开启即可。当文档中引文非常多，每次更新都会卡顿时，可以关闭此功能，添加一部分或最终手动进行更新。
## 插入参考文献
{{&lt; admonition tip &#34;注意：插入参考文献时要保证Zotero在后台运行&#34; false &gt;}}

{{&lt; /admonition &gt;}}
### 设置默认引用格式
打开要插入参考文献的 Word，点击 `Zotero 选项卡`-&gt;`Document Reference`，设置参考文献默认引用格式为 GB/T 7714-2015
![设置参考文献默认引用格式为GB/T 7714-2015](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202404011523027.png)

### 插入单篇文献
在 Word 正文中点击要插入参考文献的位置，然后在`Zotero 选项卡`中点击`Add/Edit Citation`，从 Zotero 中选择要插入的参考文献，点击`OK`即可插入。
![插入单篇参考文献](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202404011533996.gif)
### 插入参考文献引用列表
在 Word 正文中点击要插入参考文献引用列表的位置，然后在`Zotero 选项卡`中点击`Add/Edit Bibliography`，即可出现参考文献引用列表。
![插入参考文献引用列表](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202404011537854.gif)
### 插入多篇参考文献
只需要在插入参考文献时，选择`多重来源`，逐个添加参考文献到右边侧栏，然后点击`OK`即可。
![插入多篇参考文献](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202404011540011.gif)

### 删除或更换多重来源
选中 Word 中多重引用的位置，在`Zotero 选项卡`中点击`Add/Edit Citation`。
左箭头：删除其中一个文献；右箭头：添加一个文献。
上、下箭头：对引文重新排序。
![删除或更换多重来源](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202404011544296.gif)
## 设置参考文献格式
Zotero 插入的参考文献引用列表，默认使用了 Word 中的**书目**样式。因此，只需要修改**书目**样式为学校要求的参考文献格式，就能保证刷新后不改变，且格式与学校要求保持一致。
NEU **硕士**毕业论文参考文献的格式要求如下：
![NEU硕士毕业论文参考文献格式要求](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202404011619038.png)

将**书目**样式修改为如上格式后，再次插入或刷新参考文献，格式就会保持此样式不变。
也可以从 [NEU Zotero 参考文献格式 Word分享](https://github.com/leegical/Blog_img/releases/tag/NEU-citation)中下载已经改好样式的 Word 文件。
![NEU-zotero-citation](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202404011625496.png)
## 注意事项
### 等与 et al
如果英文文献作者超过3个，但显示为中文的`等`，而不是英文 `et al`，需要手动将英文文献信息中的 `语言` 字段修改为 `en`。同理，将中文文献的 `语言` 字段修改为 `zh-CN`。
![修改文献语言](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202404012026213.png)
### 文献名大小写
有些期刊或出版社（如 ACS）导出的文章题目（Title）是每个实词的首字母是大写，如：
- **Measurement-Based Probabilistic Timing Analysis for Multi-path Programs**

但一些杂志或学校要求是句子（Sentence）格式，即只是题目的首字母大写（缩写除外，都是大写），如：
- **Measurement-based probabilistic timing analysis for multi-path programs**

修改方法有两种。
#### 单一文献手动修改
选中文章，然后在右侧文章信息 `信息/Info` 中 `标题/Title` 字段处右击，选择 `句首大写/Transform Text-Sentence case`，然后再把缩略语等需要大写的手动修改一下。
![手动句首大写](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202404012054249.gif)
#### 批量修改
批量转为句首字母大写，即 Sentence 模式的实现方法参考如下链接：
{{&lt; link &#34;https://zhuanlan.zhihu.com/p/283889592&#34; &#34;Zotero批量文章题目大小写转为首字母大写的方法（含视频）&#34; &#34;Zotero批量文章题目大小写转为首字母大写的方法（含视频）&#34; true &gt;}}

操作有风险，建议先备份库再进行下面的操作。
1. 选中需要转换的文献，本例中为4条全选。
2. 在Zotero中依次点击：Zotero&gt;Tools&gt;Developer&gt;Run Javascript
![运行js](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202404012100166.png)

3.在弹出的对话框中将以下代码复制进去：
```js
zoteroPane = Zotero.getActiveZoteroPane();
items = zoteroPane.getSelectedItems();
var result = &#34;&#34;;
for (item of items) {
    var title = item.getField(&#39;title&#39;);
    result &#43;= &#34; &#34; &#43; title &#43; &#34;\n&#34;;
    var new_title = title.replace(/\b([A-Z][a-z0-9]&#43;|A)\b/g, function (x) { return x.toLowerCase(); });
    new_title = new_title.replace(/(^|\?\s*)[a-z]/, function (x) { return x.toUpperCase(); });
    result &#43;= &#34;-&gt; &#34; &#43; new_title &#43; &#34;\n\n&#34;;
    // Do it at your own risk
    item.setField(&#39;title&#39;, new_title);
    await item.saveTx();
}
return result;
```

4. 点击Run，右侧会显示题目的修改情况。
![Run js](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202404012101922.png)

5. 关闭此窗口，则在Zotero主窗口发现已经修改完成，都成为句首字母大写，最好再核实一下，如果有不正确的，手动再修改一下。
![句首字母大写效果](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202404012101563.png)

---

> 作者: [云吱](https://haoyep.com/)  
> URL: https://haoyep.com/posts/word-zotero-citation/  


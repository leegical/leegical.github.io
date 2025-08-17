# 在 Word 中使用 Zotero 插入参考文献

本文介绍了如何在 Word 中使用 Zotero 插入参考文献，并设定东北大学要求的参考文献引用列表格式。

<!--more-->

## 准备工作
### 参考文献引用格式
安装 GB/T 7714-2015 参考文献引用格式。
#### Zotero 官方7714样式（不推荐）
> [!WARNING]
> 此官方格式存在一些问题，如不能区分中英文文献，导致引用英文文献也是“等”，而不是“et al”。因此并不推荐。

1. 打开 Zotero，点击`编辑`->`首选项`->`引用`
2. 在`样式`中点击`获取更多样式`
3. 搜索`7714`即可安装国标引用样式。注意有1987、2005和2015三个时间，note、author-date 和 numeric 三个格式，鼠标悬停即可预览样式
![安装Zotero 官方7714样式](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311071542774.png)
#### 比较贴近 NEU 要求的7714样式
Github 上的[Chinese-STD-GB-T-7714-related-csl]( https://github.com/redleafnew/Chinese-STD-GB-T-7714-related-csl "Chinese-STD-GB-T-7714-related-csl")仓库（或[Gitee 镜像仓库]( https://gitee.com/redleafnew00/Chinese-STD-GB-T-7714-related-csl "Gitee")）提供7714 2015的官方样式及众多修改版，其中[002gb]( https://github.com/redleafnew/Chinese-STD-GB-T-7714-related-csl/blob/main/002gb-t-7714-2015-numeric-bilingual-no-uppercase-no-url-doi.csl "002gb")样式比较符合东北大学的要求，除了网络文献的引用顺序有点差异。
![002gb样式](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311071542161.png)

1. 点击 \[[Github](https://raw.githubusercontent.com/redleafnew/Chinese-STD-GB-T-7714-related-csl/main/002gb-t-7714-2015-numeric-bilingual-no-uppercase-no-url-doi.csl) | [Gitee](https://gitee.com/redleafnew00/Chinese-STD-GB-T-7714-related-csl/raw/main/002gb-t-7714-2015-numeric-bilingual-no-uppercase-no-url-doi.csl) \]下载引用格式文件
2. 打开 Zotero，依次进入`编辑`->`首选项`->`引用`
3. 点击`+`号添加样式。选中已下载的002 csl 样式，打开。
![导入样式](https://cdn.haoyep.com/gh/leegical/Blog_img/md_img202311071542053.png)
>会提示`***.csl不是一个有效的 CSL 1.0.2 样式文件，你可能不能和Zotero一起正常工作`，不用管，点击 OK 继续导入。
![不管提示，继续导入](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202404011457740.png)

4. 点击 OK 保存退出首选项。然后重新打开`编辑`->`首选项`->`导出`—>**条目格式**，设置成刚才导入的7714样式
![设置默认导出样式](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202404011502945.png)
### 在 Word 中安装 Zotero 插件
1. 关闭所有已经打开的 Word
2. 打开 Zotero，点击`编辑`->`首选项`->`引用`
3. 在`文档编辑软件`中点击`安装加载项 Microsoft Word`，记得勾选`使用经典版"添加引注"`
![安装加载项 Microsoft Word](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202404011508777.png)

## Zotero Word 插件选项卡
![Zotero Word 插件选项卡](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202404061347758.png)

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
> [!IMPORTANT]
> 注意：插入参考文献时要保证Zotero在后台运行。

### 设置默认引用格式
打开要插入参考文献的 Word，点击 `Zotero 选项卡`->`Document Reference`，设置参考文献默认引用格式为 GB/T 7714-2015
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
![NEU硕士毕业论文参考文献格式要求](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202404061323866.png)

将**书目**样式修改为如上格式后，再次插入或刷新参考文献，格式就会保持此样式不变。
也可以从 [NEU Zotero 参考文献格式 Word分享](https://github.com/leegical/Blog_img/releases/tag/NEU-citation)中下载已经改好样式的 Word 文件。
![NEU-zotero-citation](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202404011625496.png)
## 注意事项
### 等与 et al
如果英文文献作者超过3个，但显示为中文的`等`，而不是英文 `et al`。这是没有设置文献语言的原因。
![英文但显示等](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202404061329315.png)

需要手动将英文文献信息中的 `语言` 字段修改为 `en`。同理，将中文文献的 `语言` 字段修改为 `zh-CN`。
![修改文献语言](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202404012026213.png)

你也可以使用[茉莉花插件](https://www.haoyep.com/posts/zotero-config/#%E5%8A%9F%E8%83%BD-1)实现自动识别语言。只需要全选文献——右键——小工具——**Auto:智能识别语言**，就可以自动更新文献语言。
![Auto:智能识别语言](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202404061333176.png)
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
{{< link "https://zhuanlan.zhihu.com/p/283889592" "Zotero批量文章题目大小写转为首字母大写的方法（含视频）" "Zotero批量文章题目大小写转为首字母大写的方法（含视频）" true >}}

操作有风险，建议先备份库再进行下面的操作。
1. 选中需要转换的文献，本例中为4条全选。
2. 在Zotero中依次点击：Zotero>Tools>Developer>Run Javascript
![运行js](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202404012100166.png)

3.在弹出的对话框中将以下代码复制进去：
```js
zoteroPane = Zotero.getActiveZoteroPane();
items = zoteroPane.getSelectedItems();
var result = "";
for (item of items) {
    var title = item.getField('title');
    result += " " + title + "\n";
    var new_title = title.replace(/\b([A-Z][a-z0-9]+|A)\b/g, function (x) { return x.toLowerCase(); });
    new_title = new_title.replace(/(^|\?\s*)[a-z]/, function (x) { return x.toUpperCase(); });
    result += "-> " + new_title + "\n\n";
    // Do it at your own risk
    item.setField('title', new_title);
    await item.saveTx();
}
return result;
```

4. 点击Run，右侧会显示题目的修改情况。
![Run js](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202404012101922.png)

5. 关闭此窗口，则在Zotero主窗口发现已经修改完成，都成为句首字母大写，最好再核实一下，如果有不正确的，手动再修改一下。
![句首字母大写效果](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202404012101563.png)

### 交叉引用
Zotero 在 Word 中参考文献的上标并不是超链接/交叉引用格式，因此无法点击上标跳转到具体参考文献列表条目。可以通过 Word 中的宏实现交叉引用。
> 参考教程：[Zotero 和 Word 参考文献与文末引用条目的超链接设置](https://zhuanlan.zhihu.com/p/674910734)

1. 打开Word -> 视图 -> 宏，选择**查看宏**
![查看宏](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202404232108298.png)
2. 输入宏名：`ZoteroLinkCitation`，点击**创建**宏
![创建宏ZoteroLinkCitation](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202404232111552.png)
3. 将代码全部替换为：
```vba
Public Sub ZoteroLinkCitation()
    
' get selected area (if applicable)
    Dim nStart&, nEnd&
    nStart = Selection.Start
    nEnd = Selection.End
    
' toggle screen updating
    Application.ScreenUpdating = False
    
' define variables
    Dim title As String
    Dim titleAnchor As String
    Dim style As String
    Dim fieldCode As String
    Dim numOrYear As String
    Dim pos&, n1&, n2&, n3&

    ActiveWindow.View.ShowFieldCodes = True
    Selection.Find.ClearFormatting
 
' find the Zotero bibliography
    With Selection.Find
        .Text = "^d ADDIN ZOTERO_BIBL"
        .Replacement.Text = ""
        .Forward = True
        .Wrap = wdFindContinue
        .Format = False
        .MatchCase = False
        .MatchWholeWord = False
        .MatchWildcards = False
        .MatchSoundsLike = False
        .MatchAllWordForms = False
    End With
    Selection.Find.Execute
    
    ' add bookmark for the Zotero bibliography
    With ActiveDocument.Bookmarks
        .Add Range:=Selection.Range, name:="Zotero_Bibliography"
        .DefaultSorting = wdSortByName
        .ShowHidden = True
    End With
    
    ' loop through each field in the document
    For Each aField In ActiveDocument.Fields
        ' check if the field is a Zotero in-text reference
        '##################################################
        If InStr(aField.Code, "ADDIN ZOTERO_ITEM") > 0 Then
            fieldCode = aField.Code
            '#############
            ' Prepare
            ' Plain citation== Format of Textfield shown
            ' must be in Brackets
            Dim plain_Cit As String
            plCitStrBeg = """plainCitation"":""["
            plCitStrEnd = "]"""
            n1 = InStr(fieldCode, plCitStrBeg)
            n1 = n1 + Len(plCitStrBeg)
            n2 = InStr(Mid(fieldCode, n1, Len(fieldCode) - n1), plCitStrEnd) - 1 + n1
            plain_Cit = Mid$(fieldCode, n1 - 1, n2 - n1 + 2)
            'Reference 'as shown' in word as a string
            
            'Title array in fieldCode (all referenced Titles within this field)
            Dim array_RefTitle(32) As String
            i = 0
            Do While InStr(fieldCode, """title"":""") > 0
                n1 = InStr(fieldCode, """title"":""") + Len("""title"":""")
                n2 = InStr(Mid(fieldCode, n1, Len(fieldCode) - n1), """,""") - 1 + n1
                If n2 < n1 Then 'Exception the type 'Article'
                    n2 = InStr(Mid(fieldCode, n1, Len(fieldCode) - n1), "}") - 1 + n1 - 1
                End If
                array_RefTitle(i) = Mid(fieldCode, n1, n2 - n1)
                fieldCode = Mid(fieldCode, n2 + 1, Len(fieldCode) - n2 - 1)
                i = i + 1
            Loop
            Titles_in_Cit = i
            
            'Number array with References shown in PlainCit
            'Numer is equal or less than Titels, depending on the type
            '[3], [8]-[10]; [2]-[4]; [2], [4], [5]
            ' All citations have to be in Brackets each! [3], [8] not [3, 8]
            ' This doesnt work otherwise!
            ' --> treatment of other delimiters could be implemented here
            Dim RefNumber(32) As String
            i = 0
            Do While (InStr(plain_Cit, "]") Or InStr(plain_Cit, "[")) > 0
                n1 = InStr(plain_Cit, "[")
                n2 = InStr(plain_Cit, "]")
                RefNumber(i) = Mid(plain_Cit, n1 + 1, n2 - (n1 + 1))
                plain_Cit = Mid(plain_Cit, n2 + 1, Len(plain_Cit) - (n2 + 1) + 1)
            i = i + 1
            Loop
            Refs_in_Cit = i
            'treat only the shown references (skip the rest)
            '[3], [8]-[10] --> skip [9]
            'Order of titles given from fieldcode, not checked!
            If Titles_in_Cit > Refs_in_Cit Then
                array_RefTitle(Refs_in_Cit - 1) = array_RefTitle(Titles_in_Cit - 1)
                i = 1
                Do While Refs_in_Cit + i <= Titles_in_Cit
                    array_RefTitle(Refs_in_Cit + i - 1) = ""
                    i = i + 1
                Loop
            End If
            
            '#############
            'Make the links
            For Refs = 0 To Refs_in_Cit - 1 Step 1
                title = array_RefTitle(Refs)
                array_RefTitle(Refs) = ""
                ' make title a valid bookmark name
                titleAnchor = title
                titleAnchor = MakeValidBMName(titleAnchor)
                
                ActiveWindow.View.ShowFieldCodes = False
                Selection.GoTo What:=wdGoToBookmark, name:="Zotero_Bibliography"
                
                '' locate the corresponding reference in the bibliography
                '' by searching for its title
                Selection.Find.ClearFormatting
                With Selection.Find
                    .Text = Left(title, 255)
                    .Replacement.Text = ""
                    .Forward = True
                    .Wrap = wdFindContinue
                    .Format = False
                    .MatchCase = False
                    .MatchWholeWord = False
                    .MatchWildcards = False
                    .MatchSoundsLike = False
                    .MatchAllWordForms = False
                End With
                Selection.Find.Execute
                               
                ' select the whole caption (for mouseover tooltip)
                Selection.MoveStartUntil ("["), Count:=wdBackward
                Selection.MoveEndUntil (vbBack)
                lnkcap = "[" & Selection.Text
                lnkcap = Left(lnkcap, 70)
                
                ' add bookmark for the reference within the bibliography
                Selection.Shrink
                With ActiveDocument.Bookmarks
                    .Add Range:=Selection.Range, name:=titleAnchor
                    .DefaultSorting = wdSortByName
                    .ShowHidden = True
                End With
                
                ' jump back to the field
                aField.Select
                ' find and select the numeric part of the field which will become the hyperlink
                Selection.Find.ClearFormatting
                With Selection.Find
                    .Text = RefNumber(Refs)
                    .Replacement.Text = ""
                    .Forward = True
                    .Wrap = wdFindContinue
                    .Format = False
                    .MatchCase = False
                    .MatchWholeWord = False
                    .MatchWildcards = False
                    .MatchSoundsLike = False
                    .MatchAllWordForms = False
                End With
                Selection.Find.Execute
                        
                numOrYear = Selection.Range.Text & ""
                                    
                ' store current style这一行如果不注释可能会存在格式变化
                ' style = Selection.style
                
                ' Generate the Hyperlink -->Forward!
                ActiveDocument.Hyperlinks.Add anchor:=Selection.Range, Address:="", SubAddress:=titleAnchor, ScreenTip:=lnkcap, TextToDisplay:="" & numOrYear
                
                ' reset the style这一行如果不注释可能会存在格式变化
                ' Selection.style = style

                ' comment if you want standard link style
                aField.Select
                With Selection.Font
                     .Underline = wdUnderlineNone
                     .Color = wdColorBlack
                End With
                    
            Next Refs 'References in Cit

        End If  'If Zotero-Field
        '#########################

        Next aField ' next field

        ' go back to original range selected
        ActiveWindow.View.ShowFieldCodes = False
        ActiveDocument.Range(nStart, nEnd).Select
        
    End Sub
    Function MakeValidBMName(strIn As String)
        Dim pFirstChr As String
        Dim i As Long
        Dim tempStr As String
        strIn = Trim(strIn)
        pFirstChr = Left(strIn, 1)
        If Not pFirstChr Like "[A-Za-z]" Then
            strIn = "A_" & strIn
        End If
        For i = 1 To Len(strIn)
            Select Case Asc(Mid$(strIn, i, 1))
            Case 49 To 57, 65 To 90, 97 To 122
                tempStr = tempStr & Mid$(strIn, i, 1)
            Case Else
                tempStr = tempStr & "_"
            End Select
            Next i
            tempStr = Replace(tempStr, "  ", " ")
            MakeValidBMName = Left(tempStr, 40)
        End Function
```
4. Ctrl+s 保存，左下角重命名为 ZoteroLinkCitation，关闭页面，并关闭 Word
![重命名宏](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202404232116706.png)
5. 重新打开 Word -> 视图 -> 宏，选择`ZoteroLinkCitation`，点击运行即可
![运行宏ZoteroLinkCitation](https://cdn.haoyep.com/gh/leegical/Blog_img/cdnimg/202404232119280.png)

---

> 作者: [Leehow](https://www.haoyep.com/)  
> URL: https://www.haoyep.com/posts/word-zotero-citation/  


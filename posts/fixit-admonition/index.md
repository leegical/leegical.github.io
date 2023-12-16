# Fixit自带的admonition样式


<!--more-->

## admonition样式
[Fixit](https://hugoFixit.com/zh-cn/)提供了admonition shortcode，支持 12 种样式，可以在页面中插入提示的横幅。代码如下：

```markdown
{{</* admonition */>}}
一个 **注意** 横幅
{{</* /admonition */>}}

{{</* admonition abstract */>}}
一个 **摘要** 横幅
{{</* /admonition */>}}

{{</* admonition info */>}}
一个 **信息** 横幅
{{</* /admonition */>}}

{{</* admonition tip */>}}
一个 **技巧** 横幅
{{</* /admonition */>}}

{{</* admonition success */>}}
一个 **成功** 横幅
{{</* /admonition */>}}

{{</* admonition question */>}}
一个 **问题** 横幅
{{</* /admonition */>}}

{{</* admonition warning */>}}
一个 **警告** 横幅
{{</* /admonition */>}}

{{</* admonition failure */>}}
一个 **失败** 横幅
{{</* /admonition */>}}

{{</* admonition danger */>}}
一个 **危险** 横幅
{{</* /admonition */>}}

{{</* admonition bug */>}}
一个 **Bug** 横幅
{{</* /admonition */>}}

{{</* admonition example */>}}
一个 **示例** 横幅
{{</* /admonition */>}}

{{</* admonition quote */>}}
一个 **引用** 横幅
{{</* /admonition */>}}
```

### 效果展示
{{< admonition >}}
一个 **注意** 横幅
{{< /admonition >}}

{{< admonition abstract >}}
一个 **摘要** 横幅
{{< /admonition >}}

{{< admonition info >}}
一个 **信息** 横幅
{{< /admonition >}}

{{< admonition tip >}}
一个 **技巧** 横幅
{{< /admonition >}}

{{< admonition success >}}
一个 **成功** 横幅
{{< /admonition >}}

{{< admonition question >}}
一个 **问题** 横幅
{{< /admonition >}}

{{< admonition warning >}}
一个 **警告** 横幅
{{< /admonition >}}

{{< admonition failure >}}
一个 **失败** 横幅
{{< /admonition >}}

{{< admonition danger >}}
一个 **危险** 横幅
{{< /admonition >}}

{{< admonition bug >}}
一个 **Bug** 横幅
{{< /admonition >}}

{{< admonition example >}}
一个 **示例** 横幅
{{< /admonition >}}

{{< admonition quote >}}
一个 **引用** 横幅
{{< /admonition >}}

### 命名参数
`admonition` shortcode 有以下命名参数:

* **type** *[可选]* (**第一个**位置参数)

    `admonition` 横幅的类型, 默认值是 `note`.

* **title** *[可选]* (**第二个**位置参数)

    `admonition` 横幅的标题, 默认值是 **type** 参数的值.

* **open** *[可选]* (**第三个**位置参数) {{< version 0.2.0 changed >}}

    横幅内容是否默认展开, 默认值是 `true`.

一个 `admonition` 示例:

```markdown
{{</* admonition type=tip title="This is a tip" open=false */>}}
一个 **技巧** 横幅
{{</* /admonition */>}}
或者
{{</* admonition tip "This is a tip" false */>}}
一个 **技巧** 横幅
{{</* /admonition */>}}
```

呈现的输出效果如下:

{{< admonition tip "This is a tip" false >}}
一个 **技巧** 横幅
{{< /admonition >}}

---

> 作者: [云吱](https://haoyep.com/)  
> URL: https://haoyep.com/posts/fixit-admonition/  


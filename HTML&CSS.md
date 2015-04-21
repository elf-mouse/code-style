# HTML/CSS 通用规则

1. [编码规则](#编码规则)
2. [代码格式](#代码格式)
3. [元数据规则](#元数据规则)

## 编码规则

1.1 __省略外链资源  URL 协议部分__

省略外链资源（图片及其它媒体资源）URL 中的 `http` / `https` 协议，使 URL 成为相对地址，避免 [Mixed Content](https://developer.mozilla.org/en-US/docs/Security/MixedContent) 问题，减小文件字节数。

__其它协议（`ftp` 等）的 URL 不省略。__

```html
<!-- Recommended -->
<script src="//www.google.com/js/gweb/analytics/autotrack.js"></script>

<!-- Not recommended -->
<script src="http://www.google.com/js/gweb/analytics/autotrack.js"></script>
```

```css
/* Recommended */
.example {
  background: url(//www.google.com/images/example);
}

/* Not recommended */
.example {
  background: url(http://www.google.com/images/example);
}
```

__在同一网站中，推荐使用相对路径链接资源，并避免使用层级过深的文件夹，以提高文件查找效率、减小文件体积。__

## 代码格式

2.1 __缩进__

CSS（包括 Less 等扩展语言）中缩进 __2 个空格__（因模板、Less 等嵌套问题，将代码缩进定为两个空格，避免代码过长）。

__不要__使用 `Tab` 或者 `Tab`、空格混搭（大多编辑器都支持把 `Tab` 定义为希望的空格数）。

```html
<ul>
  <li>Fantastic</li>
  <li>Great</li>
</ul>
```

```css
.example {
  color: blue;
}
```

2.2 __一律使用小写字母__

```html
<!-- Recommended -->
<img src="google.png" alt="Google">

<!-- Not recommended -->
<A HREF="/">Home</A>
```

```css
/* Recommended */
color: #e5e5e5;

/* Not recommended */
color: #E5E5E5;
```

2.3 __删除行尾空格__

## 元数据规则

3.1 __文件编码__

__使用不带 BOM 的 UTF-8 编码。__

* 在 HTML中指定编码 `<meta charset="utf-8">`；
* 无需使用 `@charset` 指定样式表的编码，它默认为 UTF-8 （参考 [@charset](https://developer.mozilla.org/en-US/docs/Web/CSS/@charset)）；
* 引用第三方 JS 文件时 `<script charset="">` 标签应指明外链文件编码，以避免不同编码文件混合使用时页面乱码。

```html
<meta charset="UTF-8">
```

3.2 __注释__

__根据需要尽可能解释代码。__

用注释来解释代码：它包括什么，它的目的是什么，它能做什么，为什么使用这个解决方案，还是说只是因为个人偏好？

（本规则根据实际项目而定，主要取决于项目的复杂程度。）

3.3 __未完成条目__

用 `TODO` 标记待办事项和活动的条目。

* 只用 TODO 来强调代办事项， 不要用其他的常见格式，例如 @@ 。
* 附加联系人（用户名或电子邮件），用括号括起来，例如 `TODO(contact)` 。
* 可在冒号之后附加活动条目说明等信息，例如 `TODO: 活动条目说明` 。

```html
<!-- TODO(john.doe): revisit centering -->
<center>Test</center>

<!-- TODO: remove optional tags -->
<ul>
  <li>Apples</li>
  <li>Oranges</li>
</ul>
```

```css
/* TODO: remove IE hacks */
.nav {
  _width: 1%;
}
```

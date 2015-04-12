# HTML 风格指南

1. [编码规则](#编码规则)
2. [代码格式](#代码格式)

## 编码规则

1.1 **文档类型（DTD）使用 HTML5**

    <!DOCTYPE html>

1.2 **语言属性**

根据 HTML5 规范：

> 强烈建议为 `html` 元素指定 `lang` 属性，从而为文档设置正确的语言。这将有助于语音合成工具确定其所应该采用的发音，有助于翻译工具确定其翻译时所应遵守的规则等等。

更多关于 `lang` 属性的知识可以从[此规范](http://www.w3.org/html/wg/drafts/html/master/semantics.html#the-html-element)中了解。

这里列出了[语言代码表](http://reference.sitepoint.com/html/lang-codes)。

1.3 **IE 兼容模式设置为 `Edge`**

IE 支持通过 `<meta>` 标签来设置渲染前页面所应该采用的 IE 版本。除非有特殊需求，否则最好是设置为 `Edge`。

    <meta http-equiv="X-UA-Compatible" content="IE=Edge">

更多细节参考[此文](http://stackoverflow.com/questions/6771258/whats-the-difference-if-meta-http-equiv-x-ua-compatible-content-ie-edge-e)。

1.4 **HTML 有效性**

编写有效的 HTML 代码，能通过[代码校验工具](http://validator.w3.org/nu/)验证。使用符合 HTML5 规范的标签，不允许使用废弃的标签，如`<font>`、`<center>`等。

- [HTML5 新增标签及废弃标签列表](http://www.w3schools.com/tags/default.asp)
- [HTML5 element list](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/HTML5/HTML5_element_list)
- [HTML5 Differences from HTML4](http://www.w3.org/TR/html5-diff/)

HTML:

    <!-- Recommended -->
    <!doctype html>
    <html lang="en">
    <head>
      <meta charset="UTF-8">
      <title>Document</title>
    </head>
    <body>
      <article>This is only a test.</article>
    </body>
    </html>

    <!-- Not recommended -->
    <title>Test</title>
    <article>This is only a test.</article>

1.5 **语义化**

- 根据 HTML 各元素设计的用途使用他们。这事关可访性、重用以及代码效率，例如 `h1-h6` 用于标题，`<p>` 用于段落，`<a>` 用于链接。
- 使用 HTML5 语义化标签。

HTML:

    <!-- Recommended -->
    <a href="recommendations/">All recommendations</a>

    <!-- Not recommended -->
    <div onclick="goToRecommendations();">All recommendations</div>

1.6 **多媒体内容提供后备方案**

- 图片添加 `alt` 属性；视频、音频添加标题和文案说明。
- 备选内容是保障可访性的重要途径。
- 无法立即在 CSS 里设置的纯装饰图片将 `alt` 属性设置为空：`alt=""`。

HTML:

    <!-- Recommended -->
    <img src="spreadsheet.png" alt="Spreadsheet screenshot." />

    <!-- Not recommended -->
    <img src="spreadsheet.png" />

1.7 **关注分离：结构、表现、行为分离。**

严格保持结构 （标记），表现 （样式），和行为 （脚本）分离, 并尽量让三者之间的交互保持在最低限度。

- 确保文档和模板只包含 HTML 结构， 所有表现都放到样式表里，所有行为都放到脚本里；
- 尽量将脚本和样式合并到一个文件，减少外链。

关注分离对于可维护性至关重要，修改 HTML（结构）要比修改样式、脚本花费更多成本。

    <!-- Recommended -->
    <!DOCTYPE html>
    <title>My first CSS-only redesign</title>
    <link rel="stylesheet" href="default.css">
    <h1>My first CSS-only redesign</h1>
    <p>I’ve read about this on a few sites but today I’m actually
    doing it: separating concerns and avoiding anything in the HTML of
    my website that is presentational.</p>
    <p>It’s awesome!</p>

    <!-- Not recommended -->
    <!DOCTYPE html>
    <title>HTML sucks</title>
    <link rel="stylesheet" href="base.css" media="screen">
    <link rel="stylesheet" href="grid.css" media="screen">
    <link rel="stylesheet" href="print.css" media="print">
    <h1 style="font-size: 1em;">HTML sucks</h1>
    <p>I’ve read about this on a few sites but now I’m sure:
        <u>HTML is stupid!!1</u>
    <center>I can’t believe there’s no way to control the styling of
    my website without doing everything all over again!</center>

1.8 **不要用 HTML 实体**

使用 UTF-8 作为文件编码时，不需要使用 HTML 实体引用，如`&mdash;`、`&rdquo;`、`&#x263a;`。
在 HTML 文档中具有特殊含义的字符（如 `<` 和 `&`）例外，控制或不可见字符也例外（如不换行空格）。

    <!-- Recommended -->
    The currency symbol for the Euro is “€”.

    <!-- Not recommended -->
    The currency symbol for the Euro is &ldquo;&eur;&rdquo;.

1.9 **保留可选标签，保持结构完整性**

[HTML5 规范](http://www.whatwg.org/specs/web-apps/current-work/multipage/syntax.html#syntax-tag-omission)定义了一些标签可以省略，以保持代码简洁性。但我们要求保持结构的完整，不省略可省标签，闭合所有元素，以避免不同浏览器环境下不可预知的问题出现。

- `<br>`, `<hr>`, `<img>`, `<input>` 等自闭合（self-closing）标签都应该在结尾添加 `/`；
- 不要省略可选的结束标签（closing tag）（例如 `</li>` 或 `</body>`）。

HTML:

    <!-- Recommended -->
    <!DOCTYPE html>
    <html>
    <head>
      <title>Spending money, spending bytes</title>
    </head>
    <body>
      <p>Sic.</p>
      <img src="xxx.jpg" alt="xxx" />
    </body>
    </html>

    <!-- Not Recommended -->
    <!DOCTYPE html>
    <title>Saving money, saving bytes</title>
    <p>Qed.
    <img src="xxx" >

1.10 **省略样式表和脚本的  `type` 属性**

使用 CSS 的样式表、使用 JavaScript 的脚本都不需要添加 `type` 属性。HTML5 默认按照 `text/css` 及 `text/javascript` 解析，兼容较老的浏览器。

    <!-- Recommended -->
    <link rel="stylesheet" href="//www.google.com/css/maia.css">

    <!-- Not recommended -->
    <link rel="stylesheet" href="//www.google.com/css/maia.css" type="text/css">

    <!-- Recommended -->
    <script src="//www.google.com/js/gweb/analytics/autotrack.js"></script>

    <!-- Not recommended -->
    <script src="//www.google.com/js/gweb/analytics/autotrack.js" type="text/javascript"></script>

- [The link element](http://www.w3.org/TR/2011/WD-html5-20110525/semantics.html#the-link-element)
- [The style element](http://www.w3.org/TR/2011/WD-html5-20110525/semantics.html#the-style-element)
- [The script element](http://www.w3.org/TR/2011/WD-html5-20110525/scripting-1.html#the-script-element)

1.11 **HTML 属性顺序**

HTML 属性应当按照以下给出的顺序依次排列，确保代码的易读性。

- `class`
- `id`, `name`
- `data-*`
- `src`, `for`, `type`, `href`
- `title`, `alt`
- `aria-*`, `role`

Class 用于标识高度可复用组件，因此应该排在首位。id 用于标识具体组件，排在第二位。

1.12 **布尔值属性**

HTML5 规范中 `disabled`、`checked`、`selected` 等属性不用设置值（[via](https://html.spec.whatwg.org/multipage/infrastructure.html#boolean-attributes)）

    <input type="text" disabled>
    <input type="checkbox" value="1" checked>
    <select>
      <option value="1" selected>1</option>
    </select>

如果非要赋值，不要使用 `true`、`false`，值必须是空字符串或属性的规范名称，且不要在末尾添加空格。

    <input type="checkbox" checked name="cheese" disabled="disabled">
    /* or */
    <input type="checkbox" checked name="cheese" disabled="">

1.13 **JavaScript 生成的标签**

通过 JavaScript 生成的标签让内容变得不易查找、编辑，并且降低性能。能避免时尽量避免。

1.14 **其他细节**

- 使用 `<ul>`、`<ol>`、`<dl>` 组织列表，不要使用一堆 `<div>` 或者 `<p>`；
- 每个包含附加文字的表单输入框都应该利用 `<label>` 标签，特别是 `radio`、`checkbox`元素；
- 使用 `<label>` 标签包裹 `radio` / `checkbox`，不需要设置 `for` 属性；
- 避免写关闭标签注释，如 `<!-- /.element -->`，大多编辑器都支持开闭标签高亮；
- 不要手动设置 `tabindex`，浏览器会自动设置顺序。

## 代码格式

2.1 **基本格式**

每个块级、列表、表格元素单独占一行，每个子元素都相对父元素缩进。

    <blockquote>
      <p><em>Space</em>, the final frontier.</p>
    </blockquote>
    
    <ul>
      <li>Moe</li>
      <li>Larry</li>
      <li>Curly</li>
    </ul>
    
    <table>
      <thead>
        <tr>
          <th scope="col">Income</th>
          <th scope="col">Taxes</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>$ 5.00</td>
          <td>$ 4.50</td>
        </tr>
      </tbody>
    </table>

**纯文本在 HTML 标签结束之前不要换行。**

2.2 **表格**

恰当地使用 `<thead>`, `<tfoot>`, `<tbody>`, `<th>` 标签（注意：出于速度考虑，`<tfoot>` 应放在 `<tbody>`，以便在所有表格数据渲染完成之前显示 `<tfoot>`）。

    <table summary="This is a chart of invoices for 2011.">
      <thead>
        <tr>
          <th scope="col">Table header 1</th>
          <th scope="col">Table header 2</th>
        </tr>
      </thead>
      <tfoot>
        <tr>
          <td>Table footer 1</td>
          <td>Table footer 2</td>
        </tr>
      </tfoot>
      <tbody>
        <tr>
          <td>Table data 1</td>
          <td>Table data 2</td>
        </tr>
      </tbody>
    </table>

2.3 **HTML 属性值使用双引号**

不要省略属性值的引号，应始终添加双引号。

    <!-- Recommended -->
    <a class="maia-button maia-button-secondary">Sign in</a>

    <!-- Not recommended -->
    <a class='maia-button maia-button-secondary'>Sign in</a>

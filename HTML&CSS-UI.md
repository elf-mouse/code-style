# HTML/CSS 编写注意事项

1. [基本原则](#基本原则)
2. [模块化编写实践](#模块化编写实践)
3. [命名注意事项](#命名注意事项)
4. [CSS 编写注意事项](#CSS 编写注意事项)

## 基本原则

- 以 `your-namespace` 为命名空间
- 关注分离，将 HTML、CSS 解耦；模块化编码。

## 模块化编写实践

- **语义化的模块名**，通过模块名应该能一眼就看出模块的是干什么的。

- **模块内部的类名继承自父级。**

HTML:

    <div class="ns-box">
      <h2 class="ns-box-hd">About the Site</h2>
      <p class="ns-box-bd">This is my blog where I talk about only the bestest things in the whole wide world.</p>
    </div>

上面的代码中，模块的名为 `box`，模块最外层使用 `{命名空间}-{模块名}` 的方式命名 Class。模块子元素以在此基础上进行命名。如果不继承父级的类名，很容易造成命名冲突。

- **充分考虑结构的语义化。**
虽然在 Class 的命名上已经做到的了关注分离，编写样式不再依赖具体的元素名称，但仍应该考虑语义化，根据元素设计的目的来使用元素。是段落的，你就用 `<p>`；是标题的，就用 `<h1>~<h6>`；是引用的，就用 `<blockquote>`，而不是简单粗暴的用 `<div>`、`<span>`。语义化的目的，一方面是抽去 CSS 以后，页面还是一个结构良好、可读的页面；另一方面，这也是 SEO 的最基本要求。

- **避免不必要的 CSS 选择符嵌套。**Class 已经模块化命名，从类名上已经可以清晰的分辨元素的从属，一般情况下也不会造成类名冲突，没有必要再进行选择器嵌套，保持 css 结构清晰，提高渲染效率。特殊情况可以嵌套（如提高权重、主题之间代码隔离），但应避免过多层级。

CSS:

    /* 推荐写法 */
    .ns-box {
      border: 1px solid #333;
    }

    .ns-box-hd {
      margin: 0;
      padding: 5px 10px;
      border-bottom: 1px solid #333;
      background-color: #CCC;
    }

    .ns-box-bd {
      margin: 10px;
    }

    /* 不推荐写法 */
    .ns-box .ns-box-hd {}
    .ns-box .ns-box-bd {}

- **与 JS 交互时，在模块 HTML 结构的最外一层添加状态，而非给模块每个子元素单独添加元素。**给最外层添加状态类以后，整个模块的样式都能控制，减少操作，提高性能。

比如，可以这样写：

    <div class="ns-box ns-box-active">
      <h3 class="ns-box-title"></h3>
      <p class="ns-box-content"></p>
    </div>

但不要这样写（效率更低）：

    <div class="ns-box">
      <h3 class="ns-box-title ns-box-title-active"></h3>
      <p class="ns-box-content ns-box-content-active"></p>
    </div>

## 命名注意事项

- 语义化，望文见义

如 `ns-tab`、`ns-nav`，不要使用 `red`、`left` 等表象的词命名。

- 模块状态 `{命名空间}-{模块名}-{状态描述}`

常用状态有：hover, current, selected, disabled, focus, blur, checked, success, error 等

- 子模块 `{命名空间}-{模块名}-{子模块名}`

常用模块名有：bd(body)，cnt(content)，hd(header)，text(txt)，img(images/pic)，title，item，cell 等， 词义表达组件要实现的功能。

- 模块嵌套

HTML:

    <ul class="ns-nav">
      <li class="ns-nav-item">
        <a href="#">nav Triggle Link</a>
        <ul class="ns-subnav">
          <li class="ns-subnav-item">
            <a href="#">subNav Triggle Link</a>
            <ul class="ns-list">

- **统一命名风格**（使用相同名词命名不同组件的子元素）：如 ns-tab-hd, ns-modal-hd，便于理解。

## CSS 编写注意事项

4.1 **不要添加浏览器厂商前缀**

使用 [Autoprefixer](https://github.com/postcss/autoprefixer) 自动添加浏览器厂商前缀，编写 CSS 时**不要添加浏览器前缀**，直接使用标准的 CSS 编写（也不要使用 mixins.less 里的前缀 mixin）。

**特别说明**

- **一些浏览器的私有属性可以添加浏览器前缀：** `-moz-appearance`, `-webkit-appearance` 等

更多使用问题参见 [Autoprefixer FAQ](https://github.com/postcss/autoprefixer#faq)。

4.2 **需要特别注意的 Class**

两个表示状态的 class：

- `.ns-active` - 激活
- `.ns-disabled` - 禁用

**不要单独使用、直接在里面编写样式！！！**

    /* 可以嵌套用 */
    .ns-nav .ns-active {
      ...
    }

    /* 可以堆叠用 */
    .ns-btn.ns-active {
      ...
    }

    /* 绝不要单独用！！！ */
    .ns-active {
      color: red;
    }

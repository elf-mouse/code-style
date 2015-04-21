# 文件编码

* 使用不带 BOM 的 `UTF-8` 编码。

# JavaScript 语言规范

## 1. 使用[严格模式](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Strict_mode)

```javascript
'use strict';

// code here
```

## 2. 语句的结尾总是使用分号

```javascript
var foo = bar; // semicolon here.

var foo = function() {
  return true;
};  // semicolon here.

function foo() {
  return true;
}  // no semicolon here.
```

## 3. 变量使用前必须使用 `var` 声明

## 4. 块内函数声明

不要在块内声明一个函数（严格模式会报语法错误）。如果确实需要在块中定义函数，可以使用函数表达式来声明函数。

```javascript
/* Recommended */
if (x) {
  var foo = function() {};
}

/* Wrong */
if (x) {
  function foo() {}
}
```

## 5. 异常

可以使用，抛出错误，而不是字符串。

## 6. 自定义异常

恰当的时候可以使用。

## 7. 标准特性总是由于非标准特性

优先使用原生的方法，而不是自行封装的非标准接口。

## 8. 不要封装基本类型

明确用于类型转换的场景除外。

```javascript
/* Recommended */
var x = Boolean(0);

if (x) {
  alert('hi');  // This will never be alerted.
}

typeof Boolean(0) == 'boolean';
typeof new Boolean(0) == 'object';

/* Not recommended */
var x = new Boolean(false);

if (x) {
  alert('hi');  // Shows 'hi'.
}
```

## 9. `this`

仅在构造函数、方法、闭包中使用 `this` 关键字，以避免错误的引用的。

## 10. 不要在 Array 上使用 `for-in` 循环

## 11. 不要使用关联数组

需要键值对映射时直接使用 `Obeject`。

## 12. 用 Array 和 Object 字面量代替 Array 和 Object 构造函数

```javascript
/* Recommend */
var arr = [x1, x2, x3],
    obj = {
      a: 0,
      b: 1,
      c: 2
    };

/* Not Recommend */
var arr = new Array(x1, x2),
    obj = new Object();
```

## 13. 类方法的定义

推荐把方法定义放在类的原型对象中。

```javascript
/* Recommended */
var Foo = {
  // Foo object
};

Foo.prototype.bar = function() {
  // bar method
};

/* Not recommended */
var Foo = function() {
  this.bar = function() {
    // bar method
  };
};
```

## 14. 禁止修改内置对象的原型

如 `Object.prototype`、`Array.prototype`、`Function.prototype` 等。

## 15. 闭包

可以使用，但应该谨慎。

有一点需要牢记，闭包保留了一个指向它封闭作用域的指针，所以，在给 DOM 元素附加闭包时，很可能会产生循环引用， 进一步导致内存泄漏。比如下面的代码：

```javascript
/* Wrong style */
function foo(element, a, b) {
  element.onclick = function() { /* uses a and b */ };
}
```

这里，即使没有使用 `element`，闭包也保留了 `element`、`a` 和 `b` 的引用。由于 `element` 也保留了对闭包的引用，这就产生了循环引用，导致不能被 GC 回收。可将代码重构为:

```javascript
function foo(element, a, b) {
  element.onclick = bar(a, b);
}

function bar(a, b) {
  return function() { /* uses a and b */ }
}
```

## 16. eval()

一般情况不要使用 `eval()`，使用 `JSON.parse` 解析系列化字符串。

## 17. 不要使用 `with() {}` 语句

## 18. 不要给 `setInterval` / `setTimeOut` 传递字符串

## 19. 拼接字符串

一般情况使用 `+` 操作符拼接字符串。如果存在大量的字符串拼接，推荐采用数组 `join()` 拼接字符串。

不要使用多行字符串字面量。

```javascript
/* Recommended */
var myString = 'A rather long string of English text, an error message ' +
    'actually that just keeps going and going -- an error ' +
    'message to make the Energizer bunny blush (right through ' +
    'those Schwarzenegger shades)! Where was I? Oh yes, ' +
    'you\'ve got an error and all the extraneous whitespace is ' +
    'just gravy.  Have a nice day.';

/* Not recommended */
var myString = 'A rather long string of English text, an error message \
                actually that just keeps going and going -- an error \
                message to make the Energizer bunny blush (right through \
                those Schwarzenegger shades)! Where was I? Oh yes, \
                you\'ve got an error and all the extraneous whitespace is \
                just gravy.  Have a nice day.';
```

# JavaScript 编码风格

## 1. 命名方式

1.1 __常量__

使用全大写字母，并用下划线分隔单词，形如 `CONST_NAME_LIKE_THIS`；
因浏览器支持问题，不要使用 `const` [关键字](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const)。

1.2 __变量__

变量采用小驼峰式命名，如 `myVar`。

1.3 __类名__

采用大驼峰式（帕斯卡命名法）命名，如 `MyClass`。

1.4 __私有变量__

私有属性、变量和方法以下划线 `_` 开头，形如 `_privateMethod`。

1.5 __文件名__

全部使用小写字母并以 `.js` 结尾。

## 2. 自定义 `toString()` 方法

可以自定义 `toString()` 方法, 但应该确保应是成功调用且不要抛异常。

## 3. 变量延迟初始化

允许延迟变量初始化，不必在声明变量时初始化。

```javascript
var name = 'My Name',
    future;
```

## 4. 明确作用域

任何时候都要明确作用域，以提高可移植性和清晰度。例如，不要依赖作用域链中的 `window` 对象。

## 5. 代码格式

5.1 __代码长度不超过 80个字符__

5.2 __缩进__

__缩进 2 个空格__，如果使用 Tab，需要把 Tab 设置成 2 个空格。

5.3 __花括号__

始终添加花括号。

```javascript
if (something) {
  // ...
} else {
  // ...
}
```

__表示块起始的大括号，不能换行：__

```javascript
/* Recommended */
if (something) {
  // ...
} else {
  // ...
}

/* Not recommended */
if (something)
{
  // ...
}
else
{
  // ...
}
```

__不允许一行判断，一律换行__

```javascript
/* Recommended */
if (foo) {
  // do something
}

/* Not recommended */
if (foo) return
```

5.4 __数组和对象的初始化__

如果初始值不是很长，就保持写在单行上：

```javascript
var arr = [1, 2, 3];  // No space after [ or before ].
var obj = {a: 1, b: 2, c: 3};  // No space after { or before }.
```

初始值占用多行时，缩进 4 个空格。

```javascript
// Object initializer.
var inset = {
  top: 10,
  right: 20,
  bottom: 15,
  left: 12
};

// Array initializer.
this.rows_ = [
  '"Slartibartfast" <fjordmaster@magrathea.com>',
  '"Zaphod Beeblebrox" <theprez@universe.gov>',
  '"Ford Prefect" <ford@theguide.com>',
  '"Arthur Dent" <has.no.tea@gmail.com>',
  '"Marvin the Paranoid Android" <marv@googlemail.com>',
  'the.mice@magrathea.com'
];

// Used in a method call.
goog.dom.createDom(goog.dom.TagName.DIV, {
  id: 'foo',
  className: 'some-css-class',
  style: 'display:none'
}, 'Hello, world!');
```

比较长的标识符或者数值，不要为了让代码好看些而手工对齐。 如:

```javascript
/* Recommended */
CORRECT_Object.prototype = {
  a: 0,
  b: 1,
  lengthyName: 2
};

/* Not recommended */
WRONG_Object.prototype = {
  a          : 0,
  b          : 1,
  lengthyName: 2
};
```

5.5 __函数参数__

尽量让函数参数在同一行上。如果一行超过 80 字符，每个参数独占一行，并以 4 个空格缩进，或者与括号对齐，以提高可读性。尽可能不要让每行超过 80 个字符。比如：

```javascript
// Four-space, wrap at 80.  Works with very long function names, survives
// renaming without reindenting, low on space.
goog.foo.bar.doThingThatIsVeryDifficultToExplain = function(
    veryDescriptiveArgumentNumberOne, veryDescriptiveArgumentTwo,
    tableModelEventHandlerProxy, artichokeDescriptorAdapterIterator) {
  // ...
};

// Four-space, one argument per line.  Works with long function names,
// survives renaming, and emphasizes each argument.
goog.foo.bar.doThingThatIsVeryDifficultToExplain = function(
    veryDescriptiveArgumentNumberOne,
    veryDescriptiveArgumentTwo,
    tableModelEventHandlerProxy,
    artichokeDescriptorAdapterIterator) {
  // ...
};

// Parenthesis-aligned indentation, wrap at 80.  Visually groups arguments,
// low on space.
function foo(veryDescriptiveArgumentNumberOne, veryDescriptiveArgumentTwo,
             tableModelEventHandlerProxy, artichokeDescriptorAdapterIterator) {
  // ...
}

// Parenthesis-aligned, one argument per line.  Visually groups and
// emphasizes each individual argument.
function bar(veryDescriptiveArgumentNumberOne,
             veryDescriptiveArgumentTwo,
             tableModelEventHandlerProxy,
             artichokeDescriptorAdapterIterator) {
  // ...
}
```

5.6 __空行__

使用空行来划分一组逻辑上相关联的代码片段。__文件末尾空一行。__

```javascript
doSomethingTo(x);
doSomethingElseTo(x);
andThen(x);

nowDoSomethingWith(y);

andNowWith(z);

var baseP = base.prototype,
    childP;

childP = child.prototype = Object.create(baseP);
childP.constructor = child;
childP._super = baseP;

if (properties) {
  extend(childP, properties);
}
```

5.7 __二元和三元操作符__

操作符始终写在前一行, 以免分号的隐式插入产生预想不到的问题。如果一行放不下, 还是按照上述的缩进风格来换行。

```javascript
var x = a ? b : c;  // All on one line if it will fit.

// Indentation +4 is OK.
var y = a ?
    longButSimpleOperandB : longButSimpleOperandC;

// Indenting to the line position of the first operand is also OK.
var z = a ?
        moreComplicatedB :
        moreComplicatedC;
```

__`.` 操作符也是如此：__

```javascript
var x = foo.bar().
    doSomething().
    doSomethingElse();
```

5.8 __空格__

* 移除行末的空格；
* 调用函数的时候，函数名与左括号之间没有空格；
* 参数序列和圆括号之间，没有空格；
* 操作符之间空一格（就一格）；
* 所有其它语法元素和和圆括号之间，都有一个空格。

```javascript
/* Recommended */
var a = b + c;

foo(bar);

return (a+b);

if (a === 0) {
  // ...
}

function foo(b) {
  // ...
}

function (x) {
  // ...
}

/* Not recommended */
var a=b+c;

foo (bar)

return(a+b);

if(a === 0) {
}

function foo (b) {
  ...
}

function(x) {
  ...
}
```

5.9 __逗号位置__

```javascript
/* Recommended */

var a = 1,
    b = 3,
    c;

/* Not Recommended */

var a = 1
    ,b
    ,c;
```

## 6. 圆括号

圆括号在 JavaScript 中有两种作用，一种表示调用函数，一种表示不同的值的组合。只在必要的时候使用圆括号。

对于一元操作符（如`delete`、`typeof`、`void`），或是在某些关键词（如 `return`、`throw`、`case`、`new`）之后，不要使用括号。

## 7. 字符串

字符串使用__单引号__，只有 JSON 中的字符串属性值使用双引号。

字符串中的 HTML 属性使用双引号。

```javascript
/* Recommended */
var string = 'this is a string',
    object = {
      str: "this is a JSON string"
    };

/* Not recommended */
var string = "this is a string",
    object = {
      str: 'this is a JSON string'
    };
```

## 8. 对象

对象的最后一个属性值后面不要写逗号（某些浏览器会报错）。

```javascript
/* Recommended */
var obj = {
  a: 1,
  b: 2,
  c: 3
};

/* Not recommended */
var obj = {
  a: 1,
  b: 2,
  c: 3,
};
```

## 9. 注释

使用 [JSDoc](http://google-styleguide.googlecode.com/svn/trunk/javascriptguide.xml?showone=Comments#Comments) 的注释风格，行内注释使用 // 注释 的形式。

为方便使用第三方工具生成 API 文档，注释必须严格按照 [JSDoc 语法](http://usejsdoc.org/)编写。

```javascript
/**
* A JSDoc comment should begin with a slash and 2 asterisks.
* Inline tags should be enclosed in braces like {@code this}.
* @desc Block tags should always start on their own line.
*/
```

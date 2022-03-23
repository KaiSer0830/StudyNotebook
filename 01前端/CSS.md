### CSS（层叠样式表）

#### css引用优先级（4种）

1.就近原则

2.理论上：行内>内嵌>链接>导入

3.实际上：内嵌、链接、导入在同一个文件头部，谁离相应的代码近，谁的优先级高.

如果同一个css定义分布在两个css文件中，那么样式取后引入的css文件。

最好将第三方组件的css放在html靠前位置，自定义的css放到html后面位置。

1、行内方式

```html
<a style="font-size:40px;color:#000000">靠谱学院</a>
```

2、内嵌方式

```html
<head>
    <style type="text/css">
        a{
            font-size:40px;
            color:#000000;
        }
    </style>
</head>

<body>
    <a>靠谱学院</a>
</body>
```

```html
<head>
    <style type="text/css">
        *{        //代表后面所有标签应用这种格式
            font-size:40px;
            color:#000000;
        }
    </style>
</head>
```

3、链接方式

引用外部样式时需要执行以下操作：

```html
<head>
    <link rel="stylesheet" type="text/css" href="文件名.css">
</head>
```

4.导入方式.

```html
<style>
    @import url(style.css);
</style>
```

我们应尽量使用 **<link>** 标签导入外部 CSS 文件，避免或者少用使用其他三种方式。

#### link标签与import标签区别

- link 属于 HTML，通过 **<link>** 标签中的 href 属性来引入外部文件，而 **@import** 属于 CSS，所以导入语句应写在 CSS 中，要注意的是**导入语句应写在样式表的开头**，否则无法正确导入外部文件；
- 页面被加载时，link会同时被加载，而@import引用的css会等到页面加载结束后加载。
- link是html标签，因此没有兼容性，而@import只有IE5以上才能识别。
- link方式样式的权重高于@import的。

#### CSS3新属性

CSS3边框如border-radius，box-shadow等；

CSS3背景如background-size，background-origin等；

CSS3 2D，3D转换如transform等；

在布局方面新增了flex布局;

在选择器方面新增了例如first-of-type,nth-child等选择器;

在盒模型方面添加了box-sizing来改变盒模型;

在颜色方面添加透明，rbga等;

媒体查讯

CSS3动画如animation等。

#### css语义化命名及常用命名规则

CSS的命名方式：

1、**结构化命名法**；（根据位置命名）

2、**语义化命名法**。 ( 根据功能命名 )

```
结构化命名法：
根据页面中板块的位置而命名，如上图中的content-left,这时如果我们想把侧边栏sidebar放在左边，那么这时content-left板块却在右边，板块位置与其命名完全不符，那么我们这时就要修改页面中的以及CSS样式中的选择器名字了，这样会很不方便，尤其是当页面结构复杂时，一会儿left,一会儿right，这样会很不容易维护。

语义化命名法：
根据页面中模块的功能而命名，如页面头部header、导航栏nav、主体main、侧边栏sidebar、底部footer、新闻列表newsList等等，这样整个页面看起来就比较清晰了，维护起来也比较方便。

命名讲求的就是见名知义，并且还要注意避免命名冲突，尤其是一个项目由多个人完成时，对于这个问题我们可以通过在命名前面加组员代号或姓名简称来解决，具体还应根据不同团队的规范来实施。

常用的CSS文件命名规则
主要的：main.css
模块：module.css
基本共用：base.css
布局，版面：layout.css
主题：themes.css
专栏：columns.css
文字：font.css
表单：forms.css
补丁：mend.css
打印：print.css
```

#### CSS的继承性

CSS 的继承特性指的是应用在一个标签上的那些 CSS 属性被传到其子标签上。看下面的 HTML 结构：

```html
<div>
    <p></p>
</div>
```

如果 **<div>** 有个属性 **color: red**，则这个属性将被 **<p>** 继承，即 **<p>** 也拥有属性 **color: red**。

由上可见，当网页比较复杂， HTML 结构嵌套较深时，一个标签的样式将深受其祖先标签样式的影响。影响的规则是：

**CSS 优先规则1：** 最近的祖先样式比其他祖先样式优先级高。

例1：

```html
<!-- 类名为 son 的 div 的 color 为 blue -->
<div style="color: red">
    <div style="color: blue">
        <div class="son"></div>
    </div>
</div>
```

如果我们把一个标签从祖先那里继承来的而自身没有的属性叫做"祖先样式"，那么"直接样式"就是一个标签直接拥有的属性。又有如下规则：

**CSS 优先规则2：**"直接样式"比"祖先样式"优先级高。

例2：

```html
<!-- 类名为 son 的 div 的 color 为 blue -->
<div style="color: red">
    <div class="son" style="color: blue"></div>
</div>
```

#### CSS样式优先级（5种）

CSS 7 种基础的选择器：

- ID 选择器， 如 #id{}

- 类选择器， 如 .class{}

- 属性选择器， 如 a[href="segmentfault.com"]{}

- 伪类选择器， 如 :hover{}

- 伪元素选择器， 如 ::before{}

- 标签选择器， 如 span{}

- 通配选择器， 如 *{}
  
  **优先级关系：内联样式 > ID 选择器 > 类选择器 = 属性选择器 = 伪类选择器 > 标签选择器 = 伪元素选择器**

1.优先级最高的-!important

```html
<style>
    div{
        color: blue!important;
    }
</style>
```

2.行内样式（会导致回流，最好用class)

```html
<body>
    <div id="text" style="color: blue;">
        111
    </div>
</body>
```

3. ID选择器

```css
#text {
    color: blue;
}
```

4.类选择器

```css
.text {
    color: blue;
}
```

5.标签

```css
div p span {
    color: blue;
}
```

当一个标签同时被多个选择符选中，我们便需要确定这些选择符的优先级。我们有如下规则：

计算选择符中 ID 选择器的个数（a），计算选择符中类选择器、属性选择器以及伪类选择器的个数之和（b），计算选择符中标签选择器和伪元素选择器的个数之和（c）。按 a、b、c 的顺序依次比较大小，大的则优先级高，相等则比较下一个。若最后两个的选择符中 a、b、c 都相等，则按照"就近原则"来判断。

#### css初始化

目的：消除不同浏览器对HTML文本呈现的差异（Github上引用次数最多的necolas的通用浏览器初始化）

```css
/* Document
   ========================================================================== */

/**
 * 1. Correct the line height in all browsers.
 * 2. Prevent adjustments of font size after orientation changes in iOS.
 */

html {
  line-height: 1.15; /* 1 */
  -webkit-text-size-adjust: 100%; /* 2 */
}

/* Sections
   ========================================================================== */

/**
 * Remove the margin in all browsers.
 */

body {
  margin: 0;
}

/**
 * Render the `main` element consistently in IE.
 */

main {
  display: block;
}

/**
 * Correct the font size and margin on `h1` elements within `section` and
 * `article` contexts in Chrome, Firefox, and Safari.
 */

h1 {
  font-size: 2em;
  margin: 0.67em 0;
}

/* Grouping content
   ========================================================================== */

/**
 * 1. Add the correct box sizing in Firefox.
 * 2. Show the overflow in Edge and IE.
 */

hr {
  box-sizing: content-box; /* 1 */
  height: 0; /* 1 */
  overflow: visible; /* 2 */
}

/**
 * 1. Correct the inheritance and scaling of font size in all browsers.
 * 2. Correct the odd `em` font sizing in all browsers.
 */

pre {
  font-family: monospace, monospace; /* 1 */
  font-size: 1em; /* 2 */
}

/* Text-level semantics
   ========================================================================== */

/**
 * Remove the gray background on active links in IE 10.
 */

a {
  background-color: transparent;
}

/**
 * 1. Remove the bottom border in Chrome 57-
 * 2. Add the correct text decoration in Chrome, Edge, IE, Opera, and Safari.
 */

abbr[title] {
  border-bottom: none; /* 1 */
  text-decoration: underline; /* 2 */
  text-decoration: underline dotted; /* 2 */
}

/**
 * Add the correct font weight in Chrome, Edge, and Safari.
 */

b,
strong {
  font-weight: bolder;
}

/**
 * 1. Correct the inheritance and scaling of font size in all browsers.
 * 2. Correct the odd `em` font sizing in all browsers.
 */

code,
kbd,
samp {
  font-family: monospace, monospace; /* 1 */
  font-size: 1em; /* 2 */
}

/**
 * Add the correct font size in all browsers.
 */

small {
  font-size: 80%;
}

/**
 * Prevent `sub` and `sup` elements from affecting the line height in
 * all browsers.
 */

sub,
sup {
  font-size: 75%;
  line-height: 0;
  position: relative;
  vertical-align: baseline;
}

sub {
  bottom: -0.25em;
}

sup {
  top: -0.5em;
}

/* Embedded content
   ========================================================================== */

/**
 * Remove the border on images inside links in IE 10.
 */

img {
  border-style: none;
}

/* Forms
   ========================================================================== */

/**
 * 1. Change the font styles in all browsers.
 * 2. Remove the margin in Firefox and Safari.
 */

button,
input,
optgroup,
select,
textarea {
  font-family: inherit; /* 1 */
  font-size: 100%; /* 1 */
  line-height: 1.15; /* 1 */
  margin: 0; /* 2 */
}

/**
 * Show the overflow in IE.
 * 1. Show the overflow in Edge.
 */

button,
input { /* 1 */
  overflow: visible;
}

/**
 * Remove the inheritance of text transform in Edge, Firefox, and IE.
 * 1. Remove the inheritance of text transform in Firefox.
 */

button,
select { /* 1 */
  text-transform: none;
}

/**
 * Correct the inability to style clickable types in iOS and Safari.
 */

button,
[type="button"],
[type="reset"],
[type="submit"] {
  -webkit-appearance: button;
}

/**
 * Remove the inner border and padding in Firefox.
 */

button::-moz-focus-inner,
[type="button"]::-moz-focus-inner,
[type="reset"]::-moz-focus-inner,
[type="submit"]::-moz-focus-inner {
  border-style: none;
  padding: 0;
}

/**
 * Restore the focus styles unset by the previous rule.
 */

button:-moz-focusring,
[type="button"]:-moz-focusring,
[type="reset"]:-moz-focusring,
[type="submit"]:-moz-focusring {
  outline: 1px dotted ButtonText;
}

/**
 * Correct the padding in Firefox.
 */

fieldset {
  padding: 0.35em 0.75em 0.625em;
}

/**
 * 1. Correct the text wrapping in Edge and IE.
 * 2. Correct the color inheritance from `fieldset` elements in IE.
 * 3. Remove the padding so developers are not caught out when they zero out
 *    `fieldset` elements in all browsers.
 */

legend {
  box-sizing: border-box; /* 1 */
  color: inherit; /* 2 */
  display: table; /* 1 */
  max-width: 100%; /* 1 */
  padding: 0; /* 3 */
  white-space: normal; /* 1 */
}

/**
 * Add the correct vertical alignment in Chrome, Firefox, and Opera.
 */

progress {
  vertical-align: baseline;
}

/**
 * Remove the default vertical scrollbar in IE 10+.
 */

textarea {
  overflow: auto;
}

/**
 * 1. Add the correct box sizing in IE 10.
 * 2. Remove the padding in IE 10.
 */

[type="checkbox"],
[type="radio"] {
  box-sizing: border-box; /* 1 */
  padding: 0; /* 2 */
}

/**
 * Correct the cursor style of increment and decrement buttons in Chrome.
 */

[type="number"]::-webkit-inner-spin-button,
[type="number"]::-webkit-outer-spin-button {
  height: auto;
}

/**
 * 1. Correct the odd appearance in Chrome and Safari.
 * 2. Correct the outline style in Safari.
 */

[type="search"] {
  -webkit-appearance: textfield; /* 1 */
  outline-offset: -2px; /* 2 */
}

/**
 * Remove the inner padding in Chrome and Safari on macOS.
 */

[type="search"]::-webkit-search-decoration {
  -webkit-appearance: none;
}

/**
 * 1. Correct the inability to style clickable types in iOS and Safari.
 * 2. Change font properties to `inherit` in Safari.
 */

::-webkit-file-upload-button {
  -webkit-appearance: button; /* 1 */
  font: inherit; /* 2 */
}

/* Interactive
   ========================================================================== */

/*
 * Add the correct display in Edge, IE 10+, and Firefox.
 */

details {
  display: block;
}

/*
 * Add the correct display in all browsers.
 */

summary {
  display: list-item;
}

/* Misc
   ========================================================================== */

/**
 * Add the correct display in IE 10+.
 */

template {
  display: none;
}

/**
 * Add the correct display in IE 10.
 */

[hidden] {
  display: none;
}
```

目的：引用了阿里云css对常用标签进行基本初始化,从而达到在项目开发中直接能引用。

一般标签在浏览器中都有默认样式，例如body标签有默认的外边距，ul有默认的小黑点和内边距，前端程序员在写页面的时候会把这些默认的样式都清除掉，让所有标签的外观效果在所有浏览器表现一致，这个步骤就是css的初始化。

用法：在HTML文件中写入外链接   <link rel="stylesheet" href="normalize.css">  即可(normalize.css为创建的文件名)

```css
HTML, body, div, h1, h2, h3, h4, h5, h6, ul, ol, dl, li, dt, dd, p, blockquote,
pre, form, fieldset, table, th, td {
    border:none;
    font-family:"微软雅黑","黑体","宋体";
    font-size:14px;
    margin:0px;
    padding:0px;
    }
html,body{
    height: 100%;
    width: 100%;
    }
address, caption, cite, code, dfn, em, strong, th, var {
    font-style: normal;
    font-weight: normal;
}
a{
    text-decoration:none;
}
a:link{
    color:#fff;
}
a:visited{
    color:#fff;
}
a:hover{
    color:#fff;
}
a:active{
    color:#fff;
}
input::-ms-clear{
    display:none;
    }
input::-ms-reveal{
    display:none;
}
input{
    -webkit-appearance: none;
    margin: 0;
    outline: none;
    padding: 0;
}
input::-webkit-input-placeholder{
    color: #ccc;
}
input::-ms-input-placeholder{
    color: #ccc;
}
input::-moz-placeholder{
    color: #ccc;
}
input[type=submit],input[type=button]{
    cursor: pointer;
}
button[disabled], input[disabled] {
    cursor: default;
}
img{
    border:none;
}
ul,ol,li{
    list-style-type:none;
}
/*公共方法*/
.clear{
    clear: both;
}
.clearleft{
    clear: left;
}
.clearright{
    clear: right;
}
.floatleft{
    float: left;
}
.floatright{
    float: right;
}
.cursor{
    cursor: pointer;
}
/*背景及色值表*/
.bg000{
    background: #000;
}
.color000{
    color: #000;
}
```

#### inline-block、inline和block

1）行内元素（display:inline;），又称内联元素
特性：不能更改元素的宽高属性，大小由内容撑开，**margin左右值有效，上下值无效**，padding在水平方向垂直方向都有效，与其他元素在一行上。
常见如：a、em、b、i、span、strong、small、label等，准确的来说是行内非替换元素，特殊一点：border可设置，但不会影响文档流，而行高会影响文档流，但会自动忽视border。

2）块级元素（display:block;）
特性：独占一行，宽度继承父元素的宽度，可设置宽高内外边距等。
常见如：div、p、h标签、ul、dd、tr、pre、table等

3）行内块级元素（display:inline-block;）
特性：能设置宽度高度，margin/padding水平垂直方向都有效，前后无换行符。
常见如：img、input等，准确的来说应该称之为行内替换元素，特殊一点：设置的高度默认为行高，垂直居中。

元素有几种方法会转换行块属性？
方法一：最简单的肯定是display：block/inline/inline-block/table等
方法二：**行内元素设置float属性后，此元素的display会赋值为block**，且拥有浮动特性，原留白也会消失。
方法三：行内元素设置position属性值为absolute或fixed后，此元素的display也会赋值为block。
注意：方法二和方法三转换为块级元素后，这两种方法不会拥有块级元素的特性之一：未继承父元素的宽度。

#### vertical-align

`vertical-align` 属性设置元素的垂直对齐方式，该属性定义行内元素的基线相对于该元素所在行的基线的垂直对齐，允许指定负长度值和百分比值。这会使元素降低而不是升高，在表单元格中，这个属性会设置单元格框中的单元格内容的对齐方式。

**vertical-align属性只对行内元素有效，对块内元素无效！设置属性display: inline-block;**

【第一种用法】： 先看后面一句“在表单元格中，这个属性会设置单元格框中的单元格内容的对齐方式。”这很容易理解，如果给一个表格的 td 加一个 vertical-align:middle 的样式，表格里面的内容会垂直居中，同样的如果给一个 vertical-align:bottom 就会底部对齐，如果给一个 vertical-align:top 就会顶部对齐。

**【第二种用法】：** 该属性定义行内元素的基线相对于该元素所在行的基线的垂直对齐。假设有两个行内元素 a 和 b ，a 和 b 都是 div，当 a 加了一个 vertical-align:middle 样式之后， b 的底部（基线）就会对齐 a 的中间位置，如下图：

![](前端图片/20200801192101425.png)

如果 a 和 b 都加了一个 vertical-align:middle 样式，那么就互相对齐了对方的中间位置，也就是它们在垂直方向上的中线对齐了，如下图：

![](前端图片/2020080119280886.png)

垂直水平居中：

```html
#container {
    width: 100%;
    height: 100vh;
    text-align: center;
}

.item {
    width: 400px;
    height: 400px;
    background-color: aqua;
    vertical-align: middle;
    display: inline-block;
}

<div id="container">
    <div class="item"></div>
    <div style="height: 100%; width: 0; vertical-align: middle; display: inline-block;"></div>
</div>
```

实现下列效果：

![](前端图片/微信图片_20211019212628.png)

```html
<style>           
    img {
        vertical-align: middle;
    }
    span.sub {
        vertical-align: sub;
    }
    span.super {
        vertical-align: super;
    }
</style>

<body>
    <p>这是一个 <img src="/run/images/smiley.png" alt="Smiley"> 笑脸图标</p>
    <p>水的化学式是: H<span class="sub">2</span>O</p>
    <p>质能方程式为: E=mc<span class="super">2</span></p>
</body>
```

#### 浮动

##### 浮动特性

1、浮动定位元素会被排除在文档流之外-脱离文档流(不占据页面空间),其余的元素要上前补位 
2、浮动元素会停靠在父元素的左边或右边，或停靠在其他已浮动元素的边缘上(元素只能在当前所在行浮动) 
3、浮动元素依然位于父元素之内 
4、浮动元素处理的问题-解决多个块级元素在一行内显示的问题 

注意 
1、一行内，显示不下所有的已浮动元素时，最后一个将换行 
2、元素一旦浮动起来之后，那么宽度将变成自适应(宽度由内容决定) 
3、元素一旦浮动起来之后，那么就将变成块级元素,尤其对行内元素，影响最大 
块级元素：允许修改尺寸 
行内元素：不允许修改尺寸 
4、文本，行内元素，行内块元素时采用环绕的方式来排列的，是不会被浮动元素压在底下的，会巧妙的避开浮动元素

浮动之后会有什么样的影响？ 
由于浮动元素会脱离文档流，所以导致不占据页面空间，所以会对父元素高度带来一定影响。如果一个元素中包含的元素全部是浮动元素，那么该元素高度将变成0（高度塌陷）

##### 清除浮动(3种)

**方法一：**使用带clear属性的空元素

在浮动元素同级后使用一个空元素如<div class="clear"></div>，并在CSS中赋予.clear{clear:both;}属性即可清理浮动。亦可使用<br class="clear" />或<hr class="clear" />来进行清理。这种方法有一个非常大的致命问题，**它所在的标签，margin属性失效了**。因为div的高度为零。

**方法二：**使用CSS的overflow属性

当子元素浮动时，给浮动元素的父级样式添加overflow:hidden;或overflow:auto;可以清除浮动，另外在 IE6 中还需要触发 hasLayout ，例如为父元素设置容器宽高或设置 zoom:1。

在添加overflow属性后，浮动元素又回到了容器层，把容器高度撑起，达到了清理浮动的效果。

**方法三：**使用CSS的:after伪元素(推荐)

结合:after 伪元素（注意这不是伪类，而是伪元素，代表一个元素之后最近的元素）和 IEhack ，可以完美兼容当前主流的各大浏览器，这里的 IEhack 指的是触发 hasLayout。

给浮动元素的容器添加一个clearfix的class，然后给这个class添加一个:after伪元素实现元素末尾添加一个看不见的块元素（Block element）清理浮动。

```html
    .clearfix:after{/*伪元素是行内元素 正常浏览器清除浮动方法*/
        content: "";
        display: block;
        height: 0;
        clear:both;
        visibility: hidden;
    }
    .clearfix{
        *zoom: 1;/*ie6清除浮动的方式 *号只有IE6-IE7执行，其他浏览器不执行*/
    }

<body>
    <div class="fahter clearfix">
        <div class="big">big</div>
        <div class="small">small</div>
    </div>
    <div class="footer"></div>
</body>
```

#### 通过属性设置css格式

```html
<head>
    <meta charset="UTF-8">
    <title>创建css选择器</title>
    <style type="text/css">
        [href]{                //将有href属性的标签设置为以下样式，如果需要精确则将[href=地址]添加上
            font-size:40px;
            background-color:#000000;
        }
        a:hover{            //鼠标经过时改为以下的格式
            font-size:80px;
            background-color:#000232;
            transition-delay:150ms;                //变化的延迟时间
            transition-duration:1000ms;            //平滑变化的速度时间
            transition-property:background-color;        //需要平滑变化的属性
        }
    </style>
</head>

<!-- id是唯一标识，只能应用于一个标签上，class可以应用在多个标签上 -->
<body>
    <a href="xxx.html">靠谱学院</a>
    <a>靠谱学院</a>
</body>
```

#### 设置文本样式

```html
<head>
    <meta charset="UTF-8">
    <title>创建文本样式</title>
    <style type="text/css">
        .class1{    
            text-align:center;            //设置对齐方式为居中
            letter-sapcing:10px;        //设置字母间距
            word-spacing:20px;        //设置单词间距
            line-height:100px;        //设置行高
            text-indent:50px;        //首行缩进
            text-decoration:underline;        //设置下划线
            text-decoration:overline;        //设置上划线
            text-decoration:line-through;        //设置中间删除线
            text-transform:capitalize;        //设置首字母大写
            text-transform:uppercase;        //字母全部设置为小写
            text-transform:lowercase;        //字母全部设置为小写

            font-family:微软雅黑;        //设置字体名称
            font-style:italic;            //设置字体样式为斜体，oblique斜度要小一点
            font-variant:small-caps;        //设置为小型大写字母
            font-weight:bolder;            //设置为粗体，值需要输入100-900整百类型，数值越大字体越粗。

            <!-- 参数分别代表水平偏移,垂直偏移，模糊程度（可省略）和颜色 -->
            text-shadow:10px 10px 1px red;            //设置文本阴影
        }
    </style>
</head>

<body>
    <p class="class1">
        hello world
    </p>
</body>
```

#### 盒子模型

简介：就是用来装页面上的元素的矩形区域。CSS中的盒子模型包括IE盒子模型和标准的W3C盒子模型。

box-sizing(有3个值哦)：border-box,padding-box,content-box.

**标准盒子模型：**

![](前端图片/42498021-b4dd6a46-845d-11e8-8bd9-ac2d90985f2a.png)

**IE盒子模型：**

![](前端图片/42498075-d3496e3a-845d-11e8-919c-eb3a7866883b.png)

区别：从图中我们可以看出，这两种盒子模型最主要的区别就是width的包含范围，在标准的盒子模型中，width指content部分的宽度，在IE盒子模型中，width表示content+padding+border这三个部分的宽度，故这使得在计算整个盒子的宽度时存在着差异：

标准盒子模型的盒子宽度：左右border+左右padding+width
IE盒子模型的盒子宽度：width

在CSS3中引入了box-sizing属性，box-sizing:content-box;表示标准的盒子模型，box-sizing:border-box表示的是IE盒子模型

最后，前面我们还提到了，box-sizing:padding-box,这个属性值的宽度包含了左右padding+width

#### **display:none与visibility:hidden**

```css
//设置后，该元素在dom元素中消失，不再占用空间
display: none;

//设置后，该元素存在的空间还在，只是不可见，依然会影响到页面布局，具有继承性
visibility: hidden;
```

#### **重绘和回流**

**重绘：**不会影响页面布局的操作，比如更改颜色
如果只是改变某个元素的背景色、文字颜色、边框颜色等等不影响它周围或内部布局的属性，将只会引起浏览器repaint（重绘）。repaint的速度明显快于reflow。

**回流：**布局的改变导致需要重新构建
说到页面为什么会慢？那是因为浏览器要花时间、花精力去渲染，尤其是当它发现某个部分发生了点变化影响了布局，需要倒回去重新渲染， 该过程称为reflow（回流）。
reflow几乎是无法避免的。现在界面上流行的一些效果，比如树状目录的折叠、展开（实质上是元素的显 示与隐藏）等，都将引起浏览器的reflow。鼠标滑过、点击……只要这些行为引起了页面上某些元素的占位面积、定位方式、边距等属性的变化，都会引起它内部、周围甚至整个页面的重新渲 染。通常我们都无法预估浏览器到底会reflow哪一部分的代码，它们都彼此相互影响着。

**回流必将引起重绘，重绘不一定会引起回流**

如何避免reflow(回流)？
reflow是不可避免的，只能将reflow对性能的影响减到最小。

1.尽可能限制reflow的影响范围。需要改变元素的样式，不要通过父级元素影响子元素。最好直接加在子元素上。

2.通过设置style属性改变结点样式的话，每设置一次都会导致一次reflow。所以最好通过设置class的方式。

3.减少不必要的DOM层级（DOM depth）。改变DOM树中的一级会导致所有层级的改变，上至根部，下至被改变节点的子节点。这导致大量时间耗费在执行reflow上面。

4.避免不必要的复杂的CSS选择器，尤其是后代选择器（descendant selectors），因为为了匹配选择器将耗费更多的CPU。

5.对于多次重排的元素，比如说动画。使用绝对定位脱离文档流，使其不影响其他元素。

#### **CSS性能优化**

JS在执行会出现DOM树解析和渲染阻塞。

我们设置3G这样加载CSS慢了。

得出的结果是先解析了等加载完CSS才渲染。其实我觉得，这可能也是浏览器的一种优化机制。因为你加载css的时候，可能会修改下面DOM节点的样式，如果css加载不阻塞DOM树渲染的话，那么当css加载完之后，DOM树可能又得重新重绘或者回流了，这就造成了一些没有必要的损耗。所以我干脆就先把DOM树的结构先解析完，把可以做的工作做完，然后等你css加载完之后，在根据最终的样式来渲染DOM树，这种做法性能方面确实会比较好一点。
由上所述，我们可以得出以下结论:

**css加载不会阻塞DOM树的解析**

**css加载会阻塞DOM树的渲染**

css加载会阻塞后面js语句的执行
因此，为了避免让用户看到长时间的白屏时间，我们应该尽可能的提高css加载速度，比如可以使用以下几种方法:

1、使用CDN(因为CDN会根据你的网络状况，替你挑选最近的一个具有缓存内容的节点为你提供资源，因此可以减少加载时间)

2、对css进行压缩(可以用很多打包工具，比如webpack,gulp等，也可以通过开启gzip压缩)

3、合理的使用缓存(设置cache-control,expires,以及E-tag都是不错的，不过要注意一个问题，就是文件更新后，你要避免缓存而带来的影响。其中一个解决防范是在文件名字后面加一个版本号)

4、减少http请求数，将多个css文件合并，或者是干脆直接写成内联样式(内联样式的一个缺点就是不能缓存)

#### position（定位）

Position属性把元素放置在一个静态的，相对的，绝对的，固定的位置中。

**Static：**位置设置为static的元素，它始终处于页面流给予的位置，static元素会忽略任何top,buttom,left,right声明。

**Relative**：在使用相对定位时，无论是否进行移动，元素仍然占据原来的空间。因此，移动元素会导致它覆盖其它框。位置设置为relative的元素，可将其移至相对于其正常位置的地方，因此left：20会将元素移至元素正常位置左边20个像素的位置。

**Absolute：**绝对定位的元素的位置相对于最近的已定位父元素，如果元素没有已定位的父元素，那么它的位置相对于<html>。 absolute 定位使元素的位置与文档流无关，因此不占据空间。 absolute 定位的元素和其他元素重叠。此元素可通过left，top等属性规定。

**Fixed：**元素的位置相对于浏览器窗口是固定位置，即使窗口是滚动的它也不会移动。Fixed定位使元素的位置与文档流无关，因此不占据空间。 Fixed定位的元素和其他元素重叠。可以通过left，top，right属性来定位。

**inherit：**规定应该从父元素继承position 属性的值。

#### CSS内容溢出处理

**text-overflow属性**：

clip是修剪文本；

ellipsis为显示省略符号来表被修剪的文本；

string为使用给定的字符串来代表被修剪的文本。

#### 双边距重叠问题（外边距折叠）

多个相邻（兄弟或者父子关系）普通流的块元素垂直方向marigin会重叠

折叠的结果为：

两个相邻的外边距都是正数时，折叠结果是它们两者之间较大的值。
两个相邻的外边距都是负数时，折叠结果是两者绝对值的较大值。
两个外边距一正一负时，折叠结果是两者的相加的和。

#### Flex布局

flex 是 Flexible Box 的缩写，意为"弹性布局"。指定容器display: flex即可。

容器有以下属性：flex-direction，flex-wrap，flex-flow，justify-content，align-items，align-content。

**flex-direction**属性决定主轴的方向；

**flex-wrap**属性定义，如果一条轴线排不下，如何换行；

**flex-flow**属性是flex-direction属性和flex-wrap属性的简写形式，默认值为row nowrap；

**justify-content**属性定义了项目在主轴上的对齐方式。

**align-items**属性定义项目在交叉轴上如何对齐。

**align-content**属性定义了多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用。

项目（子元素）也有一些属性：order，flex-grow，flex-shrink，flex-basis，flex，align-self。

**order**属性定义项目的排列顺序。数值越小，排列越靠前，默认为0。

**flex-grow**属性定义项目的放大比例，默认为0，即如果存在剩余空间，也不放大。

**flex-shrink**属性定义了项目的缩小比例，默认为1，即如果空间不足，该项目将缩小。

**flex-basis**属性定义了在分配多余空间之前，项目占据的主轴空间（main size）。

flex属性是flex-grow, flex-shrink 和 flex-basis的简写，默认值为0 1 auto。后两个属性可选。

**align-self**属性允许单个项目有与其他项目不一样的对齐方式，可覆盖align-items属性。默认值为auto，表示继承父元素的align-items属性，如果没有父元素，则等同于stretch。

#### 边框渐变

第一种：border-image设置边框颜色渐变示例

```css
.box{
    width: 100px;
    height: 100px;
    border:10px solid #ddd;
    border-image: -webkit-linear-gradient(#F80, #2ED) 20 20;
    border-image: -moz-linear-gradient(#F80, #2ED) 20 20;
    border-image: -o-linear-gradient(#F80, #2ED) 20 20;
    border-image: linear-gradient(#F80, #2ED) 20 20;
}
```

第二种：border-color设置边框颜色渐变示例
border-color属性为我们提供了同一条边框设置多种颜色，但是目前为止只有Firefox 3.0+的浏览支持这个属性。所以运用或测试时我们需要加上-moz-前缀。

```css
.box {
    width: 200px;
    height: 100px;
    border: 10px solid transparent;
    border-radius: 15px 0 15px 0;
    -moz-border-top-colors:#a0a #909 #808 #707 #606 #505 #404 #303;
    -moz-border-right-colors:#a0a #909 #808 #707 #606 #505 #404 #303;
    -moz-border-bottom-colors:#a0a #909 #808 #707 #606 #505 #404 #303;
    -moz-border-left-colors:#a0a #909 #808 #707 #606 #505 #404 #303;
 }
```

#### 垂直水平居中

有一个width 200，height 200，怎么实现在屏幕上垂直水平居中？

1、采用绝对定位，原理是子绝父相，父元素设置position：relative，子元素设置position：absolute，然后通过transform或margin组合使用达到垂直居中效果，设置top：50%，left：50%，transform：translate（-50%，-50%）。

2、绝对居中，原理是当top,bottom为0时，margin-top&bottom设置auto的话会无限延伸沾满空间并平分，当left，right为0时,margin-left&right设置auto会无限延伸占满空间并平分。

```css
.center {
    background: red;
    width: 100px;
    height: 100px;
    position: absolute;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    margin: auto;
  } 
```

3、flex布局

```css
.container {        /*父样式*/
    width: 100%;
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
}

.item{        /*子样式*/
    width: 400px;
    height: 400px;
    background-color: #00FFFF;
}
```

4、采用flex，父元素设置display：flex，子元素设置margin：auto。

```html
<div style="width: 400px; height: 400px; display: flex;">
    <div style=" width: 200px; height: 200px; background-color: #00FFFF; margin: auto;"></div>
</div>
```

5、首先子元素设置display: inline-block，形成行内块级元素。父级元素设置text-align：center，子元素水平居中，然后设置display: table-cell和vertical-align： middle使其垂直居中，最后设置font-size：0消除近似居中的bug。

```html
<div style=" width: 100 ; height: 100vh;background-color: #00FFFF; text-align: center; vertical-align: middle; display: table-cell; font-size: 0;">
    <div style="width: 20px; height: 20px; display: inline-block; background-color: #FFE4C4;"></div>
</div>
```

6.vertical:middle，利用同级元素对齐

```html
#container {
    width: 100%;
    height: 100vh;
    text-align: center;
}

.item {
    width: 400px;
    height: 400px;
    background-color: aqua;
    vertical-align: middle;
    display: inline-block;
}

<div id="container">
    <div class="item"></div>
    <div style="height: 100%; width: 0; vertical-align: middle; display: inline-block;"></div>
</div>
```

7、文字居中

```css
.container {
    width: 100%;
    height: 100vh;
}

.item {
    width: 400px;
    height: 400px;
    display: table-cell;        /*此元素会作为一个表格单元格显示（类似 <td> 和 <th>）*/
    vertical-align: middle;            
    text-align: center;
}
```

#### BFC/IFC/GFC/FFC

先来了解一下常见的定位方案，定位方案是控制元素的布局，有三种常见方案:

- 普通流 (normal flow)

> 在普通流中，元素按照其在 HTML 中的先后位置至上而下布局，在这个过程中，行内元素水平排列，直到当行被占满然后换行，块级元素则会被渲染为完整的一个新行，除非另外指定，否则所有元素默认都是普通流定位，也可以说，普通流中元素的位置由该元素在 HTML 文档中的位置决定。

- 浮动 (float)

> 在浮动布局中，元素首先按照普通流的位置出现，然后根据浮动的方向尽可能的向左边或右边偏移，其效果与印刷排版中的文本环绕相似。

- 绝对定位 (absolute positioning)

> 在绝对定位布局中，元素会整体脱离普通流，因此绝对定位元素不会对其兄弟元素造成影响，而元素具体的位置由绝对定位的坐标决定。

**FC**的全称是：Formatting Contexts，是W3C CSS2.1规范中的一个概念。它是页面中的一块渲染区域，并且有一套渲染规则，它决定了其子元素将如何定位，以及和其他元素的关系和相互作用。

##### **BFC**

BFC(Block Formatting Contexts)直译为"块级格式化上下文"。Block Formatting Contexts就是页面上的一个隔离的渲染区域，容器里面的子元素不会在布局上影响到外面的元素，反之也是如此。

通俗一点来讲，可以把 BFC 理解为一个封闭的大箱子，箱子内部的元素无论如何翻江倒海，都不会影响到外部。

如何产生BFC？
（1）body 根元素
（2）float属性不为none
（3）绝对定位元素：position (absolute、fixed)
（4）display为inline-block, table-cell, table-caption, flex, inline-flex
（5）overflow 除了 visible 以外的值 (hidden、auto、scroll）

BFC的布局规则如下：
1.内部的盒子会在垂直方向，一个个地放置；
2.盒子垂直方向的距离由margin决定， 属于同一个BFC的两个相邻Box的上下margin会发生重叠；
3.每个元素的左边，与包含的盒子的左边相接触，即使存在浮动也是如此；
4.BFC的区域不会与float重叠；
5.BFC就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素，反之也如此；
6.计算BFC的高度时，浮动元素也参与计算。

**BFC 特性及应用**

**1. 盒子垂直方向的距离由margin决定，属于同一个BFC的两个相邻Box的上下margin会发生重叠**

```html
<head>
div{
    width: 100px;
    height: 100px;
    background: lightblue;
    margin: 100px;
}
</head>
<body>
    <div></div>
    <div></div>
</body>
```

![](前端图片/v2-0a9ca8952c83141250a2d9002e6d2047_r.png)

从效果上看，因为两个 div 元素都处于同一个 BFC 容器下 (这里指 body 元素) 所以第一个 div 的下边距和第二个 div 的上边距发生了重叠，所以两个盒子之间距离只有 100px，而不是 200px。

首先这不是 CSS 的 bug，我们可以理解为一种规范，**如果想要避免外边距的重叠，可以将其放在不同的 BFC 容器中。**

```html
<div class="container">
    <p></p>
</div>
<div class="container">
    <p></p>
</div>
.container {
    overflow: hidden;
}
p {
    width: 100px;
    height: 100px;
    background: lightblue;
    margin: 100px;
}
```

这时候，两个盒子边距就变成了 200px

![](前端图片/v2-5b8d6e8b2b507352900c1ece00018855_r.png)

**2. BFC 可以包含浮动的元素（清除浮动）**

我们都知道，浮动的元素会脱离普通文档流，来看下下面一个例子，当不给父节点设置高度，子节点设置浮动的时候，会发生高度塌陷，这时候就需要清除浮动。

```html
<div style="border: 1px solid #000;">
    <div style="width: 100px;height: 100px;background: #eee;float: left;"></div>
</div>
```

![](前端图片/v2-371eb702274af831df909b2c55d6a14b_r.png)

由于容器内元素浮动，脱离了文档流，所以容器只剩下 2px 的边距高度。如果使触发容器的 BFC，那么容器将会包裹着浮动元素。

```html
<div style="border: 1px solid #000;overflow: hidden">
    <div style="width: 100px;height: 100px;background: #eee;float: left;"></div>
</div>
```

效果如图：

![](前端图片/v2-cc8365db5c9cc5ca003ce9afe88592e7_720w.png)

**3. BFC 可以阻止元素被浮动元素覆盖**

先来看一个文字环绕效果：

```html
<div style="height: 100px;width: 100px;float: left;background: lightblue">我是一个左浮动的元素</div>
<div style="width: 200px; height: 200px;background: #eee">我是一个没有设置浮动, 也没有触发 BFC 元素, width: 200px; height:200px;background: #eee;</div>
```

![](前端图片/v2-dd3e636d73682140bf4a781bcd6f576b_r.png)

这时候其实第二个元素有部分被浮动元素所覆盖，(但是文本信息不会被浮动元素所覆盖) 如果想避免元素被覆盖，可触第二个元素的 BFC 特性，在第二个元素中加入 **overflow: hidden**，就会变成：

![](前端图片/v2-5ebd48f09fac875f0bd25823c76ba7fa_r.png)

这个方法可以用来实现两列自适应布局，效果不错，这时候左边的宽度固定，右边的内容自适应宽度(去掉上面右边内容的宽度)。

##### **IFC**

IFC(Inline Formatting Contexts)直译为"内联格式化上下文或者行内格式化上下文"，IFC的line box（线框）高度由其包含行内元素中最高的实际高度计算而来（不受到竖直方向的padding/margin影响)。

**影响IFC内布局的css**
font-size 

line-height 

height 

vertical-aligin

**IFC布局规则**

1.框会从包含块的顶部开始 一个接一个地水平摆放
2.摆放这些框的时候，在水平方向上的外边距、边框、内边距所占用的空间都会被考虑在内，在垂直方向上，这些框可能会以不同形式来对齐(顶部 底部或文本基线对齐)，能把在一行上的框都完全包含进去的一个矩形区域被称为该行的行框，水平的margin、padding、border有效，垂直无效，不能指定宽高
3.行框的宽度由包含块和存在的浮动来决定IFC的特性

**IFC的特性**

1.IFC中的line box一般左右都贴紧整个IFC，但是会因为float元素而扰乱，float元素会位于IFC与line box之间，使得line box宽度缩短。
2.IFC中不可能有块级元素的，当插入块级元素时(如p中插入div) 会产生两个匿名块与div分隔开，即产生两个IFC，每个IFC对外表现为块级元素与div垂直排列。

**IFC的应用**
水平居中：当一个块要在环境中水平居中时，设置子元素为inline-block则会在外层产生IFC，父元素通过text-align则可以使其水平居中。
垂直居中：创建一个IFC，用其中一个元素撑开父元素的高度，然后设置其vertical-align:middle，其他行内元素则可以在此父元素下垂直居中。

##### GFC

GFC(GridLayout Formatting Contexts)直译为"网格布局格式化上下文"，当为一个元素设置display值为grid的时候，此元素将会获得一个独立的渲染区域，我们可以通过在网格容器（grid container）上定义网格定义行（grid definition rows）和网格定义列（grid definition columns）属性各在网格项目（grid item）上定义网格行（grid row）和网格列（grid columns）为每一个网格项目（grid item）定义位置和空间。
那么GFC有什么用呢，和table又有什么区别呢？首先同样是一个二维的表格，但GridLayout会有更加丰富的属性来控制行列，控制对齐以及更为精细的渲染语义和控制。

##### **FFC**

FFC(Flex Formatting Contexts)直译为"自适应格式化上下文"，display值为flex或者inline-flex的元素将会生成自适应容器（flex container），可惜这个牛逼的属性只有谷歌和火狐支持，不过在移动端也足够了，至少safari和chrome还是OK的，毕竟这俩在移动端才是王道。
Flex Box 由伸缩容器和伸缩项目组成。通过设置元素的 display 属性为 flex 或 inline-flex 可以得到一个伸缩容器。设置为 flex 的容器被渲染为一个块级元素，而设置为 inline-flex 的容器则渲染为一个行内元素。
伸缩容器中的每一个子元素都是一个伸缩项目。伸缩项目可以是任意数量的。伸缩容器外和伸缩项目内的一切元素都不受影响。简单地说，Flexbox 定义了伸缩容器内伸缩项目该如何布局。

#### display:inline-block 显示间隙问题

**产生原因：**元素被当成行内元素排版的时候，元素之间的空白符（空格、回车换行等）都会被浏览器处理，根据white-space的处理方式（默认是normal，合并多余空白），原来HTML代码中的回车换行被转成一个空白符，在字体不为0的情况下，空白符占据一定宽度，所以inline-block的元素之间就出现了空隙。这些元素之间的间距会随着字体的大小而变化，当行内元素font-size:16px时，间距为8px。

**解决方法：**

1.移除空格
2.使用margin负值
3.使用font-size:0
4.letter-spacing——设置对象中的单词之间插入的空格数
5.word-spacing——设置对象中的文字之间的间隔.每一个中文文字以及英文字母之间

#### 字体奇偶性

```css
一般来说，使用偶数字体多于奇数字体
1.比例关系
相对来说偶数字号比较容易和页面中其他部分的字号构成一个比例关系。如我使用14px的字体作为正文字号，那么其他部分的字体（如标题）就可以使用14×1.5 =21px的字体，或者在一些地方使用到了14×0.5=7px的padding或者margin，如果你是在用sass或者less编写css，这时候用处就凸显出来了。

2.UI设计师的缘故
大多数设计师用的软件如ps提供的字号是偶数，自然到了 前端那边也是用的是偶数。

3.浏览器缘故
其一是低版本的浏览器ie6会把奇数字体强制转化为偶数，即13px渲染为14px。

其二是为了平分字体。偶数宽的汉字，如12px的汉字，去掉1像素的字体间距，填充了的字体像素宽度其实就是11px，这样的汉字中竖线左右是平分的，如“中”子，左右就是5px了。

4.系统差别
Windows 自带的点阵宋体（中易宋体）从 Vista 开始只提供 12、14、16 px 这三个大小的点阵，而 13、15、17 px 时用的是小一号的点阵（即每个字占的空间大了 1 px，但点阵没变），于是略显稀疏。

但是也可以使用奇数字体。目前来说12，13，14，15，16px都是比较常用而且不错的字号，通过审查元素可以看到知乎的正文字号和豆瓣部分栏目（豆瓣电影）也是用了13px字号，效果都很不错。使用奇数号字体不好的地方是，文本段落无法对齐。
```

#### 伪元素与伪类

单冒号（:）用于css3的伪类
双冒号（::）用于css3的伪元素

在 CSS 中伪类一直用 : 表示，如 :hover, :active 等
伪元素在CSS1中已存在，当时语法是用 : 表示，如 :before 和 :after
后来在CSS3中修订，伪元素用 :: 表示，如 ::before 和 ::after，以此区分伪元素和伪类
由于低版本IE对双冒号不兼容，开发者为了兼容性各浏览器，继续使使用 :after 这种老语法表示伪元素

想让插入的内容出现在其它内容前，使用::before，否者，使用::after；
在代码顺序上，::after生成的内容也比::before生成的内容靠后。
如果按堆栈视角，::after生成的内容会在::before生成的内容之上
::before就是以一个子元素的存在，定义在元素主体内容之前的一个伪元素。并不存在于dom之中，只存在在页面之中。:before 和 :after 这两个伪元素，是在CSS2.1里新出现的。起初，伪元素的前缀使用的是单冒号语法，但随着Web的进化，在CSS3的规范里，伪元素的语法被修改成使用双冒号，成为::before ::after

其中伪类和伪元素的根本区别在于：**它们是否创造了新的元素。**

伪元素/伪对象：不存在在DOM文档中，是虚拟的元素，是创建新元素。代表某个元素的子元素，这个子元素虽然在逻辑上存在，但却并不实际存在于文档树中。

伪类：存在DOM文档中，逻辑上存在但在文档树中却无须标识的“幽灵”分类。

#### 三栏布局

三列布局又分为两种，两列定宽一列自适应，以及两侧定宽中间自适应

##### 流体布局

什么叫流体布局？
简单的来说，就是网页缩小和放大时网页布局会随着浏览器的大小而改变！
由于页面中的宽度值都是百分数，所以拉伸、缩小浏览器的大小，布局的宽度会随之变化儿不会出现横向滚动条。这种布局叫做流体布局，可以增加文本的易读性。
但是流体布局也有缺点。在窗口宽度小的时候，行变得非常窄，很难阅读。在多列布局中尤其如此。并且，很多时候，会遇到文字溢出等情况！

##### 圣杯布局

**圣杯布局和双飞翼布局解决的问题是相同的，就是两边定宽，中间自适应的三栏布局，中间栏要在放在文档流前面以优先渲染。**

圣杯布局：为了让中间div内容不被遮挡，将中间div设置了左右padding-left和padding-right后，将左右两个div用相对布局position: relative并分别配合right和left属性，以便左右两栏div移动后不遮挡中间div。

**优点：不需要添加dom节点**

缺点：圣杯布局的缺点：正常情况下是没有问题的，但是特殊情况下就会暴露此方案的弊端，如果将浏览器无限放大时，「圣杯」将会「破碎」掉。当middle部分的宽小于left部分时就会发生布局混乱。（middle<left即会变形）

首先在 container 里面有三栏，分别是 left、middle、right，**注意这里 middle 需要放在最前面，保证可以得到优先渲染**：

```html
<div class="grail-container">
    <div class="grail-middle">
        Grail main
    </div>
    <div class="grail-left">
        Grail left
    </div>
    <div class="grail-right">
        Grail right
    </div>
</div>
```

对于 container ，设置一个属性 overflow: hidden; 让其形成一个 BFC ，然后使其三栏浮动，并使用相对定位：

```css
.grail-container {
    overflow: hidden;
}
.grail-container>div {
    position: relative;
    float: left;
    height: 100%;
}
```

这时执行以下的步骤：

　　① 置 middle 的 width: 100%，给 left 和 right 定宽度，这里假设都是 width: 200px;

　　② 这时 left 被挤到下面去了，所以我们要把它拉回来，设置 margin-left: -100%;

　　③ 还有一个 right 没有拉回来，同样，设置 margin-left: 200px;，这里的长度等于 right 自身的长度

　　④ 这时 middle 的两边被 left 和 right 给覆盖了，于是我们要把两边怼回来，设置 container padding: 0 200px 0 200px;

　　⑤ middle 怼回来了，可是 left 和 right 也跟着回来，所以现在我们要把 left 和 right 给怼回去，分别设置 left left: -200px;，right right: -200px;(这就是之前为什么要用相对定位)

```css
.grail-container {
    overflow: hidden;
    padding: 0 200px;
}
.grail-container>div {
    position: relative;
    float: left;
    height: 100%;
}
.grail-middle {
    width: 100%;
    background-color: blue;
}
.grail-left {
    width: 200px;
    background-color: green;
    margin-left: -100%;
    left: -200px;
}
.grail-right {
    width: 200px;
    background-color: brown;
    margin-left: -200px;
    right: -200px;
}
```

##### 双飞翼布局

双飞翼布局使于淘宝，是淘宝团队提出来的一种实现三栏布局的方案，其和圣杯布局是同门兄弟，同样将页面分为 header、container、footer ，不过在 container 里面有所区别。圣杯布局的缺陷在于内容区被 container 的 padding 夹在里面，使得页面宽度过小时会出现布局紊乱，这时候双飞翼布局就不使用 padding 来将内容区夹在里面，而是给内容区添加一个 main ，设置 margin 将页面主动的撑开，其 DOM 结构与圣杯类似，区别在于在 middle 中多了一个 main。

**优点：不会像圣杯布局那样变形**

缺点是：多加了一层dom节点

```html
<div class="double-wing-container">
    <div class="double-wing-middle">
        <div class="double-wing-main">
            Double wing main.
        </div>
    </div>
    <div class="double-wing-left">
        Double wing left.
    </div>
    <div class="double-wing-right">
        Double wing right
    </div>
</div>
```

```css
.double-wing-container {
    overflow: hidden;
}
.double-wing-container>div {
    position: relative;
    float: left;
    height: 100%;
}
```

这时执行与圣杯布局类似的步骤：

　　① 置 middle 的 width: 100%，给 left 和 right 定宽度，这里假设都是 width: 200px;

　　② 这时 left 被挤到下面去了，所以我们要把它拉回来，设置 margin-left: -100%;

　　③ 还有一个 right 没有拉回来，同样，设置 margin-left: 200px;，这里的长度等于 right 自身的长度

　　注意这里开始就有区别了：

　　④ 使用 main 把内容区撑开，设置 margin: 0 200px 0 200px;，同时设置 overflow: hidden; 使其形成一个 BFC

```css
.double-wing-container {
    overflow: hidden;
}
.double-wing-container>div {
    position: relative;
    float: left;
    height: 100%;
}
.double-wing-middle {
    width: 100%;
    background-color: gray;
}
.double-wing-left {
    width: 200px;
    background-color: orange;
    margin-left: -100%;
}
.double-wing-right {
    width: 200px;
    background-color: red;
    margin-left: -200px;
}
.double-wing-main {
    height: 100%;
    margin: 0 200px;
    background-color: pink;
    overflow: hidden;
}
```

##### Flex三栏布局

```html
<div class="flex-container">
    <div class="flex-middle">
        Flex main
    </div>
    <div class="flex-left">
        Flex left
    </div>
    <div class="flex-right">
        Flex right
    </div>
</div>
```

然后执行以下步骤：

　　① 设置 container 布局方式 display: flex; 

　　② 这时候设置 middle width: 100%; ，同时给两栏定宽，这里假设都是 width: 200px;

　　③ 既然是两栏固定，那么就不让两栏收缩，给 left 和 right 设置 flex-shrink: 0;

　　④ 由于 DOM 结构和我们实际的顺序不一样，这时我们来排个序 left order: 1;，middle order: 2;，right order: 3;

```css
.flex-container {
    display: flex;
}
.flex-container>div {
    height: 100%;
}
.flex-left {
    width: 200px;
    background-color: yellow;
    order: 1;
    flex-shrink: 0;
}
.flex-middle {
    width: 100%;
    background-color: gray;
    order: 2;
}
.flex-right {
    width: 200px;
    background-color: red;
    order: 3;
    flex-shrink: 0;
}
```

OK啦，现在拖动试一试。可以看出 flex 布局具有更强的适应性，在窗口宽度过小的时候不会造成页面布局混乱。通过设置内容的伸缩，可以实现任意栏的固定和自适应，同时也可以实现三栏自适应，通过设置 flex 内容的 flex-shrink 和 flex-grow 可以实现自定义的适应性布局。

#### PostCSS

```
PostCSS是什么？
PostCSS 是使用 javascript 插件转换 CSS 的后处理器。PostCSS 本身不会对你的 CSS 做任何事情，你需要安装一些 plugins 才能开始工作。这不仅使其模块化，同时功能加强。
它可以被理解为一个平台，可以让一些插件在上面跑。它提供了一个解析器，可以将CSS解析成抽象语法树。
通过PostCSS这个平台，我们能够开发一些插件，来处理CSS。热门插件如autoprefixer。

能解决什么问题？
我们用SASS来写代码，需要自己做浏览器兼容，而利用PostCSS，我们按照最简洁最惯用的写法就可以了。

PostCSS由哪些东西组成？
1. CSS Parser
2. CSS 节点树 API
3. source map 生成器
4. 生成节点树串
```

#### 高度塌陷

**产生原因：**由于浮动元素会脱离文档流，所以导致不占据页面空间，所以会对父元素高度带来一定影响。如果一个元素中包含的元素全部是浮动元素，那么该元素高度将变成0（高度塌陷）

**解决方法（6种）：**
**方案1：**直接设置父元素的高度 
优势：极其简单 
弊端：必须要知道父元素高度是多少

**方案2：**在父元素中，追加空子元素，并设置其clear属性为both，clear是css中专用于清除浮动的属性，清除当前元素前面的元素浮动所带来的影响
优势：代码量少 容易掌握 简单易懂 
弊端：会添加许多无意义的空标签，有违结构与表现的分离，不便于后期的维护

**方案3：**设置父元素浮动 
优势：简单，代码量少，没有结构和语义化问题 
弊端：对后续元素会有影响

**方案4：**为父元素设置overflow属性，取值：hidden 或 auto （利用的是BFC的特性）
优势：简单，代码量少 
弊端：如果有内容要溢出显示(弹出菜单)，也会被一同隐藏

**方案5：**父元素设置display:table 
优势：不影响结构与表现的分离，语义化正确，代码量少 
弊端：盒模型属性已经改变，会造成其他问题

**方案6：**使用内容生成的方式清除浮动
.clearfix:after {
    content:""; 
    display: block; 
    clear:both; 
}
:after 选择器向选定的元素之后插入内容 
content:""; 生成内容为空 
display: block; 生成的元素以块级元素显示, 
clear:both; 清除前面元素浮动带来的影响 
相对于空标签闭合浮动的方法 
优势：不破坏文档结构，没有副作用 
弊端：代码量多

#### 响应式布局（4种）

前端开发中，静态网页通常需要适应不同分辨率的设备，常用的自适应解决方案包括：

```
媒体查询
百分比
自适应场景下的rem解决方案
通过vw/vh来实现自适应
```

##### px和视口

**1.像素**

像素是网页布局的基础，一个像素表示了计算机屏幕所能显示的最小区域，像素分为两种类型：css像素和物理像素。

我们在js或者css代码中使用的px单位就是指的是css像素，物理像素也称设备像素，只与设备或者说硬件有关，同样尺寸的屏幕，设备的密度越高，物理像素也就越多。下表表示css像素和物理像素的具体区别：

| css像素 | 为web开发者提供，在css中使用的一个抽象单位   |
| ----- | -------------------------- |
| 物理像素  | 只与设备的硬件密度有关，任何设备的物理像素都是固定的 |

那么css像素与物理像素的转换关系是怎么样的呢？为了明确css像素和物理像素的转换关系，必须先了解视口是什么。

**2. 视口**

广义的视口，是指浏览器显示内容的屏幕区域，狭义的视口包括了布局视口、视觉视口和理想视口

(1) 布局视口（layout viewport）

布局视口定义了pc网页在移动端的默认布局行为，因为通常pc的分辨率较大，布局视口默认为980px。也就是说在不设置网页的viewport的情况下，pc端的网页默认会以布局视口为基准，在移动端进行展示。因此我们可以明显看出来，默认为布局视口时，根植于pc端的网页在移动端展示很模糊。

(2) 视觉视口（visual viewport）

视觉视口表示浏览器内看到的网站的显示区域，用户可以通过缩放来查看网页的显示内容，从而改变视觉视口。视觉视口的定义，就像拿着一个放大镜分别从不同距离观察同一个物体，视觉视口仅仅类似于放大镜中显示的内容，因此视觉视口不会影响布局视口的宽度和高度。

(3) 理想视口（ideal viewport）

理想视口或者应该全称为“理想的布局视口”，在移动设备中就是指设备的分辨率。换句话说，理想视口或者说分辨率就是给定设备物理像素的情况下，最佳的“布局视口”。

***上述视口中，最重要的是要明确理想视口的概念，在移动端中，理想视口或者说分辨率跟物理像素之间有什么关系呢？\***

为了理清分辨率和物理像素之间的联系，我们介绍一个用DPR（Device pixel ratio）设备像素比来表示，则可以写成：

```
1 DPR = 物理像素／分辨率
```

在不缩放的情况下，一个css像素就对应一个dpr，也就是说，在不缩放

```
1 CSS像素 = 物理像素／分辨率
```

此外，在移动端的布局中，我们可以通过viewport元标签来控制布局，比如一般情况下，我们可以通过下述标签使得移动端在理想视口下布局：

```
<meta id="viewport" name="viewport" content="width=device-width; initial-scale=1.0; maximum-scale=1; user-scalable=no;">
```

上述meta标签的每一个属性的详细介绍如下：

| 属性名           | 取值     | 描述                   |
| ------------- | ------ | -------------------- |
| width         | 正整数    | 定义布局视口的宽度，单位为像素      |
| height        | 正整数    | 定义布局视口的高度，单位为像素，很少使用 |
| initial-scale | [0,10] | 初始缩放比例，1表示不缩放        |
| minimum-scale | [0,10] | 最小缩放比例               |
| maximum-scale | [0,10] | 最大缩放比例               |
| user-scalable | yes／no | 是否允许手动缩放页面，默认值为yes   |

其中我们来看width属性，在移动端布局时，在meta标签中我们会将width设置称为device-width，device-width一般是表示分辨率的宽，通过width=device-width的设置我们就将布局视口设置成了理想的视口。

**3. px与自适应**

上述我们了解到了当通过viewport元标签，设置布局视口为理想视口时，1个css像素可以表示成：

```
1 CSS像素 = 物理像素／分辨率
```

我们知道，在pc端的布局视口通常情况下为980px，移动端以iphone6为例，分辨率为375 * 667，也就是说布局视口在理想的情况下为375px。比如现在我们有一个750px * 1134px的视觉稿，那么在pc端，一个css像素可以如下计算：

```
PC端： 1 CSS像素 = 物理像素／分辨率 = 750 ／ 980 =0.76 px
```

而在iphone6下：

```
iphone6：1 CSS像素 = 物理像素 ／分辨率 = 750 ／ 375 = 2 px
```

也就是说在PC端，一个CSS像素可以用0.76个物理像素来表示，而iphone6中 一个CSS像素表示了2个物理像素。此外不同的移动设备分辨率不同，也就是1个CSS像素可以表示的物理像素是不同的，因此如果在css中仅仅通过px作为长度和宽度的单位，造成的结果就是无法通过一套样式，实现各端的自适应。

##### 媒体查询

在前面我们说到，不同端的设备下，在css文件中，1px所表示的物理像素的大小是不同的，因此通过一套样式，是无法实现各端的自适应。由此我们联想：

***如果一套样式不行，那么能否给每一种设备各一套不同的样式来实现自适应的效果？\***

答案是肯定的。

使用[@media](https://github.com/media)媒体查询可以针对不同的媒体类型定义不同的样式，特别是响应式页面，可以针对不同屏幕的大小，编写多套样式，从而达到自适应的效果。举例来说：

```
@media screen and (max-width: 960px){
    body{
      background-color:#FF6699
    }
}

@media screen and (max-width: 768px){
    body{
      background-color:#00FF66;
    }
}

@media screen and (max-width: 550px){
    body{
      background-color:#6633FF;
    }
}

@media screen and (max-width: 320px){
    body{
      background-color:#FFFF00;
    }
}
```

上述的代码通过媒体查询定义了几套样式，通过max-width设置样式生效时的最大分辨率，上述的代码分别对分辨率在0～320px，320px～550px，550px～768px以及768px～960px的屏幕设置了不同的背景颜色。

通过媒体查询，可以通过给不同分辨率的设备编写不同的样式来实现响应式的布局，比如我们为不同分辨率的屏幕，设置不同的背景图片。比如给小屏幕手机设置[@2x](https://github.com/2x)图，为大屏幕手机设置[@3x](https://github.com/3x)图，通过媒体查询就能很方便的实现。

但是媒体查询的缺点也很明显，如果在浏览器大小改变时，需要改变的样式太多，那么多套样式代码会很繁琐。

##### 百分比

除了用px结合媒体查询实现响应式布局外，我们也可以通过百分比单位 " % " 来实现响应式的效果。

比如当浏览器的宽度或者高度发生变化时，通过百分比单位，通过百分比单位可以使得浏览器中的组件的宽和高随着浏览器的变化而变化，从而实现响应式的效果。

为了了解百分比布局，首先要了解的问题是：

***css中的子元素中的百分比（%）到底是谁的百分比？\***

直观的理解，我们可能会认为子元素的百分比完全相对于直接父元素，height百分比相对于height，width百分比相对于width。当然这种理解是正确的，但是根据css的盒式模型，除了height、width属性外，还具有padding、border、margin等等属性。那么这些属性设置成百分比，是根据父元素的那些属性呢？此外还有border-radius和translate等属性中的百分比，又是相对于什么呢？下面来具体分析。

**1. 百分比的具体分析**

（1）子元素height和width的百分比

子元素的height或width中使用百分比，是相对于子元素的直接父元素，width相对于父元素的width，height相对于父元素的height。比如：

```
<div class="parent">
  <div class="child"></div>
</div>
```

如果设置：
.father{
width:200px;
height:100px;
}
.child{
width:50%;
height:50%;
}
展示的效果为：

![](前端图片/41773411-91e22044-764e-11e8-8ad4-9066db87166f.png)

(2) top和bottom 、left和right

子元素的top和bottom如果设置百分比，则相对于直接非static定位(默认定位)的父元素的**高度**，

同样子元素的left和right如果设置百分比，则相对于直接非static定位(默认定位的)父元素的**宽度**。

展示的效果为：

![](前端图片/41774950-67423bfc-7654-11e8-9947-aa1621fe39f9.png)

（3）padding

子元素的padding如果设置百分比，不论是垂直方向或者是水平方向，**都相对于直接父亲元素的width**，而与父元素的height无关。

举例来说：

```
.parent{
  width:200px;
  height:100px;
  background:green;
}
.child{
  width:0px;
  height:0px;
  background:blue;
  color:white;
  padding-top:50%;
  padding-left:50%;
}
```

展示的效果为：

![](前端图片/41775365-36a0b0da-7656-11e8-8495-bd58f7ab0bf2.png)

子元素的初始宽高为0，通过padding可以将父元素撑大，上图的蓝色部分是一个正方形，且边长为100px,说明padding不论宽高，如果设置成百分比都相对于父元素的width。

（4）margin

跟padding一样，margin也是如此，子元素的margin如果设置成百分比，不论是垂直方向还是水平方向，都相对于直接父元素的width。这里就不具体举例。

（5）border-radius

border-radius不一样，如果设置border-radius为百分比，则是相对于自身的宽度，举例来说：

```
  <div class="trangle"></div>
```

设置border-radius为百分比：

```
.trangle{
  width:100px;
  height:100px;
  border-radius:50%;
  background:blue;
  margin-top:10px;
}
```

展示效果为：

![](前端图片/41775919-6a41ae42-7658-11e8-8e54-43ad05c12d43.png)

除了border-radius外，还有比如translate、background-size等都是相对于自身的，这里就不一一举例。

**2. 百分比单位布局应用**

百分比单位在布局上应用还是很广泛的，这里介绍一种应用。

比如我们要实现一个固定长宽比的长方形，比如要实现一个长宽比为4:3的长方形,我们可以根据padding属性来实现，因为padding不管是垂直方向还是水平方向，百分比单位都相对于父元素的宽度，因此我们可以设置padding-top为百分比来实现，长宽自适应的长方形：

```
<div class="trangle"></div>
```

设置样式让其自适应：

```
.trangle{
  height:0;
  width:100%;
  padding-top:75%;
}
```

通过设置padding-top：75%,相对比宽度的75%，因此这样就设置了一个长宽高恒定比例的长方形，具体效果展示如下：

[![jest](https://user-images.githubusercontent.com/17233651/41851698-52d2bd2c-78bb-11e8-97cb-26f985195809.gif)](https://user-images.githubusercontent.com/17233651/41851698-52d2bd2c-78bb-11e8-97cb-26f985195809.gif)

**3. 百分比单位缺点**

从上述对于百分比单位的介绍我们很容易看出如果全部使用百分比单位来实现响应式的布局，有明显的以下两个缺点：

（1）计算困难，如果我们要定义一个元素的宽度和高度，按照设计稿，必须换算成百分比单位。
（2）从小节1可以看出，各个属性中如果使用百分比，相对父元素的属性并不是唯一的。比如width和height相对于父元素的width和height，而margin、padding不管垂直还是水平方向都相对比父元素的宽度、border-radius则是相对于元素自身等等，造成我们使用百分比单位容易使布局问题变得复杂。

##### rem解决方案

**1. rem单位**

首先来看，什么是rem单位。rem是一个灵活的、可扩展的单位，由浏览器转化像素并显示。与em单位不同，rem单位无论嵌套层级如何，都只相对于浏览器的根元素（HTML元素）的font-size。**默认情况下，html元素的font-size为16px**，所以：

```
    1 rem = 16px
```

为了计算方便，通常可以将html的font-size设置成：

```
    html{ font-size: 62.5% }
```

这种情况下：

```
    1 rem = 10px
```

**2.通过rem来实现响应式布局**

rem单位都是相对于根元素html的font-size来决定大小的,根元素的font-size相当于提供了一个基准，当页面的size发生变化时，只需要改变font-size的值，那么以rem为固定单位的元素的大小也会发生响应的变化。
因此，如果通过rem来实现响应式的布局，只需要根据视图容器的大小，动态的改变font-size即可。

```
function refreshRem() {
    var docEl = doc.documentElement;
    var width = docEl.getBoundingClientRect().width;
    var rem = width / 10;
    docEl.style.fontSize = rem + 'px';
    flexible.rem = win.rem = rem;
}
win.addEventListener('resize', refreshRem);
```

上述代码中将视图容器分为10份，font-size用十分之一的宽度来表示，最后在header标签中执行这段代码，就可以动态定义font-size的大小，从而1rem在不同的视觉容器中表示不同的大小，用rem固定单位可以实现不同容器内布局的自适应。

**3. rem2px和px2rem**

如果在响应式布局中使用rem单位，那么存在一个单位换算的问题，rem2px表示从rem换算成px，这个就不说了，只要rem乘以相应的font-size中的大小，就能换算成px。更多的应用是px2rem，表示的是从px转化为rem。

比如给定的视觉稿为750px（物理像素），如果我们要将所有的布局单位都用rem来表示，一种比较笨的办法就是对所有的height和width等元素，乘以相应的比例，现将视觉稿换算成rem单位，然后一个个的用rem来表示。另一种比较方便的解决方法就是，在css中我们还是用px来表示元素的大小，最后编写完css代码之后，将css文件中的所有px单位，转化成rem单位。

px2rem的原理也很简单，重点在于预处理以px为单位的css文件，处理后将所有的px变成rem单位。可以通过两种方式来实现：

1） webpack loader的形式：

```
npm install px2rem-loader
```

在webpack的配置文件中：

```
module.exports = {
  // ...
  module: {
    rules: [{
      test: /\.css$/,
      use: [{
        loader: 'style-loader'
      }, {
        loader: 'css-loader'
      }, {
        loader: 'px2rem-loader',
        // options here
        options: {
          remUni: 75,
          remPrecision: 8
        }
      }]
    }]
  }
```

}

2）webpack中使用postcss plugin

```
npm install postcss-loader
```

在webpack的plugin中:

```
var px2rem = require('postcss-px2rem');

module.exports = {
  module: {
    loaders: [
      {
        test: /\.css$/,
        loader: "style-loader!css-loader!postcss-loader"
      }
    ]
  },
  postcss: function() {
    return [px2rem({remUnit: 75})];
  }
}
```

**4. rem 布局应用举例**

网易新闻的移动端页面使用了rem布局，具体例子如下：

[![jest1](https://user-images.githubusercontent.com/17233651/41913702-97d36b92-7983-11e8-8fd6-56404ce1e5ce.gif)](https://user-images.githubusercontent.com/17233651/41913702-97d36b92-7983-11e8-8fd6-56404ce1e5ce.gif)

**5. rem 布局的缺点**

通过rem单位，可以实现响应式的布局，特别是引入相应的postcss相关插件，免去了设计稿中的px到rem的计算。rem单位在国外的一些网站也有使用，这里所说的rem来实现布局的缺点，或者说是小缺陷是：

***在响应式布局中，必须通过js来动态控制根元素font-size的大小。***

也就是说css样式和js代码有一定的耦合性。且必须将改变font-size的代码放在css样式之前。

##### vw/vh

**1. 什么是vw/vh ?**

css3中引入了一个新的单位vw/vh，与视图窗口有关，vw表示相对于视图窗口的宽度，vh表示相对于视图窗口高度，除了vw和vh外，还有vmin和vmax两个相关的单位。各个单位具体的含义如下：

| 单位   | 含义                  |
| ---- | ------------------- |
| vw   | 相对于视窗的宽度，视窗宽度是100vw |
| vh   | 相对于视窗的高度，视窗高度是100vh |
| vmin | vw和vh中的较小值          |
| vmax | vw和vh中的较大值          |

这里我们发现视窗宽高都是100vw／100vh，那么vw或者vh，下简称vw，很类似百分比单位。vw和%的区别为：

| 单位    | 含义                                                |
| ----- | ------------------------------------------------- |
| %     | 大部分相对于祖先元素，也有相对于自身的情况比如（border-radius、translate等) |
| vw/vh | 相对于视窗的尺寸                                          |

从对比中我们可以发现，vw单位与百分比类似，单确有区别，前面我们介绍了百分比单位的换算困难，这里的vw更像"理想的百分比单位"。任意层级元素，在使用vw单位的情况下，1vw都等于视图宽度的百分之一。

**2. vw单位换算**

同样的，如果要将px换算成vw单位，很简单，只要确定视图的窗口大小（布局视口），如果我们将布局视口设置成分辨率大小，比如对于iphone6/7 375*667的分辨率，那么px可以通过如下方式换算成vw：

```
1px = （1/375）*100 vw
```

此外，也可以通过postcss的相应插件，预处理css做一个自动的转换，[postcss-px-to-viewport](https://github.com/evrone/postcss-px-to-viewport)可以自动将px转化成vw。
postcss-px-to-viewport的默认参数为：

```
var defaults = {
  viewportWidth: 320,
  viewportHeight: 568, 
  unitPrecision: 5,
  viewportUnit: 'vw',
  selectorBlackList: [],
  minPixelValue: 1,
  mediaQuery: false
};
```

通过指定视窗的宽度和高度，以及换算精度，就能将px转化成vw。

**3. vw/vh单位的兼容性**

可以在https://caniuse.com/ 查看各个版本的浏览器对vw单位的支持性。

[![2018-06-27 8 19 53](https://user-images.githubusercontent.com/17233651/41973430-82f1b8fe-7a47-11e8-8aab-f371ea3c6bd1.png)](https://user-images.githubusercontent.com/17233651/41973430-82f1b8fe-7a47-11e8-8aab-f371ea3c6bd1.png)

从上图我们发现，绝大多数的浏览器支持vw单位，但是ie9-11不支持vmin和vmax，考虑到vmin和vmax单位不常用，vw单位在绝大部分高版本浏览器内的支持性很好，但是opera浏览器整体不支持vw单位，如果需要兼容opera浏览器的布局，不推荐使用vw。

#### CSS动画

```html
<head>
    <meta charset="UTF-8">
    <title>创建动画</title>
    <style type="text/css">
        p{
            width:100px;
            height:100px;
            background-color:antiquewhite;
        }
        p:hover{
            animation-duration:500ms;
            animation-delay:200ms;
            animation-name:kaopu; 
            animation-iteration-count:infinite;            //动画效果无限循环，可以取数值
            animation-direction:alternate;            //反方向再变化


            animation-fill-mode:forwards;            //在动画最后一帧停止，与前面的不能同时设置
            //如果动画需要隐藏文字则可以利用设置opacity来实现
        }
        @keyframes kaopu{
               from{                     //初始变化时的效果
                width:150px;
                height:150px;
                background-color:#ffad2a;
            }   
            50%{                    //变化到一半的效果
                width:130px;
                height:130px;
                background-color:#ffad2a;                
            }
            75%{                    //变化到四分之三的效果
                width:160px;
                height:160px;
                background-color:#ffad2a;                 
            }
            to{                        //最终变化的效果
                width:200px;
                height:200px;
                background-color:#ffad2a;
            }
        }
    </style>
</head>
```

#### Js动画与CSS动画的区别

Chromium项目里，渲染线程分为main thread和compositor thread。

如果CSS动画只是改变`transforms`和`opacity`，这时整个CSS动画得以在compositor thread完成（而JS动画则会在main thread执行，然后触发compositor进行下一步操作）。

在JS执行一些昂贵的任务时，main thread繁忙，CSS动画由于使用了compositor thread可以保持流畅。

```
在主线程中，维护了一棵Layer树（LayerTreeHost），管理了TiledLayer，在compositor thread，维护了同样一颗LayerTreeHostImpl，管理了LayerImpl，这两棵树的内容是拷贝关系。因此可以彼此不干扰，当Javascript在main thread操作LayerTreeHost的同时，compositor thread可以用LayerTreeHostImpl做渲染。当Javascript繁忙导致主线程卡住时，合成到屏幕的过程也是流畅的。
为了实现防假死，鼠标键盘消息会被首先分发到compositor thread，然后再到main thread。这样，当main thread繁忙时，compositor thread还是能够响应一部分消息，例如，鼠标滚动时，加入main thread繁忙，compositor thread也会处理滚动消息，滚动已经被提交的页面部分（未被提交的部分将被刷白）。
```

CSS动画比JS流畅的前提：

- 在Chromium基础上的浏览器中
- JS在执行一些昂贵的任务
- 同时CSS动画不触发layout或paint。在CSS动画或JS动画触发了paint或layout时，需要main thread进行Layer树的重计算，这时CSS动画或JS动画都会阻塞后续操作。

现今CSS动画和JS动画主要的**不同点**是：

1.功能涵盖面，JS比CSS3大

​    1.1 定义动画过程的`@keyframes`不支持递归定义，如果有多种类似的动画过程，需要调节多个参数来生成的话，将会有很大的冗余（比如jQuery Mobile的动画方案），而JS则天然可以以一套函数实现多个不同的动画过程。    

​    1.2 时间尺度上，`@keyframes`的动画粒度粗，而JS的动画粒度控制可以

​    1.3 CSS3动画里被支持的时间函数非常少，不够灵活

​    1.4 以现有的接口，CSS3动画无法做到支持两个以上的状态转化

2.实现/重构难度不一，CSS3比JS更简单，性能调优方向固定

3.对于帧速表现不好的低版本浏览器，CSS3可以做到自然降级，而JS则需要撰写额外代码

4.CSS动画有天然事件支持（`TransitionEnd`、`AnimationEnd`，但是它们都需要针对浏览器加前缀），JS则需要自己写事件

5.CSS3有兼容性问题，而JS大多时候没有兼容性问题

#### transition和animation的区别

​        animation 可以用 name 设置动画的名称，用 duration 设置动画完成的周期，用 timing-function 设置动画的速度曲线，delay 设置动画什么时候开始，iteration-count 设置动画播放的次数，direction 规定下一个周期是否逆向的播放，play-state 动画是否正在进行或者暂停，fill-mode 设置动画停了之后位置什么状态

　　transition 用 property 去设置过渡效果的属性名称，duration 设置过渡效果的周期，timing-function 规定速度效果的速度曲线，delay 设定过渡效果什么时候开始；

区别：

1、transition 是过渡，是样式值的变化的过程，只有开始和结束；animation 其实也叫关键帧，通过和 keyframe 结合可以设置中间帧的一个状态，可能是多个状态；

![](前端图片/v2-15379cd306eb8b478091d47c683d1747_r.jpg)

2、animation 配合 @keyframe 可以自动显示动画效果，而 transition 需要通过 hover 或者 js 事件来配合触发；

3、animation 可以设置很多的属性，比如循环次数，动画结束的状态等等，transition 只能触发一次；

4、animation 可以结合 keyframe 设置每一帧，但是 transition 只有两帧；

5、在性能方面：浏览器有一个主线程和排版线程；主线程一般是对 js 运行的页面布局生成位图等等，然后把生成好的位图传递给排版线程，而排版线程会通过 GPU 将位图绘制到页面上，也会向主线程请求位图等等；我们在用使用 aniamtion 的时候这样就可以改变很多属性，像我们改变了 width、height、postion 等等这些改变文档流的属性的时候就会引起页面的回流和重绘，对性能影响就比较大，但是我们用 transition 的时候一般会结合 tansfrom 来进行旋转和缩放等不会生成新的位图，当然也就不会引起页面的重排了

Transition 强调**过渡**，Transition ＋ Transform ＝ 两个关键帧的Animation

Animation 强调**流程与控制**，Duration ＋ TransformLib ＋ Control ＝ 多个关键帧的Animation

如果只有两个关键帧我会选择Transition ＋ Transform

#### base64

所谓Base64，就是说选出64个字符----小写字母a-z、大写字母A-Z、数字0-9、符号"+"、"/"（再加上作为垫字的"="，实际上是65个字符）----作为一个基本字符集。然后，其他所有符号都转换成这个字符集中的字符。

Base64是一种可逆的编码方式，是一种用64个Ascii字符来表示任意二进制数据的方法。

具体来说，转换方式可以分为四步。

> 第一步，将每三个字节作为一组，一共是24个二进制位。
> 
> 第二步，将这24个二进制位分为四组，每个组有6个二进制位。
> 
> 第三步，在每组前面加两个00，扩展成32个二进制位，即四个字节。
> 
> 第四步，根据下表，得到扩展后的每个字节的对应符号，这就是Base64的编码值。

```
0　A　　 17　R　　　34　i　　　51　z

1　B　　 18　S　　　35　j　　　52　0

2　C　　 19　T　　　36　k　　　53　1

3　D　　 20　U　　　37　l　　　54　2

4　E　　 21　V　　　38　m　　　55　3

5　F　　 22　W　　　39　n　　　56　4

6　G　　 23　X　　　40　o　　　57　5

7　H　　 24　Y　　　41　p　　　58　6

8　I　　 25　Z　　　42　q　　　59　7

9　J　　 26　a　　　43　r　　　60　8

10　K　　27　b　　　44　s　　　61　9

11　L　　28　c　　　45　t　　　62　+

12　M　　29　d　　　46　u　　　63　/

13　N　　30　e　　　47　v

14　O　　31　f　　　48　w　　　

15　P　　32　g　　　49　x

16　Q　　33　h　　　50　y
```

因为，Base64将三个字节转化成四个字节，因此Base64编码后的文本，**会比原文本大出三分之一左右**。

举一个具体的实例，演示英语单词Man如何转成Base64编码。

```
第一步，"M"、"a"、"n"的ASCII值分别是77、97、110，对应的二进制值是01001101、01100001、01101110，将它们连成一个24位的二进制字符串010011010110000101101110。

第二步，将这个24位的二进制字符串分成4组，每组6个二进制位：010011、010110、000101、101110。

第三步，在每组前面加两个00，扩展成32个二进制位，即四个字节：00010011、00010110、00000101、00101110。它们的十进制值分别是19、22、5、46。

第四步，根据上表，得到每个值对应Base64编码，即T、W、F、u。
```

如果字节数不足三，则这样处理：

> a）二个字节的情况：将这二个字节的一共16个二进制位，按照上面的规则，转成三组，最后一组除了前面加两个0以外，后面也要加两个0。这样得到一个三位的Base64编码，再在末尾补上一个"="号。
> 
> 比如，"Ma"这个字符串是两个字节，可以转化成三组00010011、00010110、00000100以后，对应Base64值分别为T、W、E，再补上一个"="号，因此"Ma"的Base64编码就是TWE=。

> b）一个字节的情况：将这一个字节的8个二进制位，按照上面的规则转成二组，最后一组除了前面加二个0以外，后面再加4个0。这样得到一个二位的Base64编码，再在末尾补上两个"="号。
> 
> 比如，"M"这个字母是一个字节，可以转化为二组00010011、00010000，对应的Base64值分别为T、Q，再补上二个"="号，因此"M"的Base64编码就是TQ==。

**优点**:可以将二进制数据转化为可打印字符，方便传输数据，对数据进行简单的加密，肉眼安全，减少了HTTP请求。
**缺点**：内容编码后体积变大，编码和解码需要额外工作量。

#### 单个问题汇总

------

##### flex属性的优缺点

灵活但是兼容性方面不强。

------

##### line-height和height的区别

line-height一般是指布局里面一段文字上下行之间的高度，是针对字体来设置的，height一般是指容器的整体高度。

------

##### 设置一个元素的背景颜色，背景颜色会填充哪些区域？

background-color设置的背景颜色会填充元素的content、padding、border区域。

------

##### CSS画三角形

需要显示哪条边赋值颜色，其余的赋值transparent。原理是边框均分。

```css
#triangle02{
    width:0;
    height:0;
    border-top:10px solid red;
    border-right:10px solid transparent;
    border-bottom:10px solid transparent;
    border-left:10px solid transparent;
}
```

------

##### CSS画长宽等比矩形

比如我们要实现一个固定长宽比的长方形，比如要实现一个长宽比为4:3的长方形,我们可以根据padding属性来实现，因为padding不管是垂直方向还是水平方向，百分比单位都相对于父元素的宽度，因此我们可以设置padding-top为百分比来实现，长宽自适应的长方形：

```
<div class="trangle"></div>
```

设置样式让其自适应：

```
.trangle{
  height:0;
  width:100%;
  padding-top:75%;
}
```

通过设通过设置padding-top：75%,相对比宽度的75%，因此这样就设置了一个长宽高恒定比例的长方形，具体效果展示如下：

![jest](https://user-images.githubusercontent.com/17233651/41851698-52d2bd2c-78bb-11e8-97cb-26f985195809.gif)](

------

##### 画一条0.5px的线

1.采用meta viewport的方式

```html
<meta name="viewport" content="width=device-width, initial-scale=0.5, minimum-scale=0.5, maximum-scale=0.5"/>
```

2.采用transform: scale()的方式

```css
transform: scale(0.5,0.5);
```

------

##### float的元素，display是什么

display为block

------

##### 隐藏页面中某个元素的方法（5种）

display:none; 

visibility:hidden;

opacity: 0;

position移到外部；

z-index涂层遮盖等等

---

##### scroll设置

参数是scroll时候，必会出现滚动条。  
参数是auto时候，子元素内容大于父元素时出现滚动条。  
参数是visible时候，溢出的内容出现在父元素之外。  
参数是hidden时候，溢出隐藏。

------

##### 设置背景颜色

在使用点运算符时，浏览器看到“-”就没法正确解析了，在那种情况下，只能将该变量使用驼峰命名法来表示。而使用方括号表示法，"-"被理解为字符串中的内容，该字符串能被正确解析。

```js
inputElement.style.backgroundColor = 'red'; 		// 这是没问题的
inputElement.style.background-color = 'red'; 		// 这是错的，浏览器看不懂啊...
inputElement.style["background-color"] = 'red'; 	// 这也是可以的
```

------


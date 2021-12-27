#### Scss常用语法



**Sass**是成熟、稳定、强大的**CSS预处理器**，而SCSS是Sass3版本当中引入的新语法特性，完全兼容CSS3的同时继承了Sass强大的动态功能。

scss是sass的一个升级版本，完全兼容sass之前的功能，又有了些新增能力。



##### scss与sass的区别

**scss采用的是｛｝语法**

**sass采用的是缩进语法，不带分号**

```scss
/*scss多行注释需要左右都有*和斜杠
by kaiser*/

//单行双斜杠
//单行双斜杠

@import "base"
 
@import alert {
	color: #000;
}

.alert-warning {
    @include alert;
}

ul {
    font-size: 15px;
    li {
        color: #ffffff;
    }
}
```

```sass
/*  sass多行注释右边没有*和斜杠
	by kaiser

//  单行只有一个双斜杠
    单行只有一个双斜杠

@import base

=alert 
	color: #000

.alert-warning {
    +alert
}

ul 
    font-size: 15px
    li 
        color: #ffffff
```



##### 变量-Variable

**区分大小写**

```scss
$primary-color: #000000;

div {
	background-color: $primary-color;
}
```



##### 嵌套时调用父选择器

```scss
//代表style1中所有的子样式都附带hover样式，父选择器style1是不带hover样式的

style1 {
	background-color: #ffffff;
	:hover {
		background-color: #000000;
	}
}

//&代表父选择器附带hover样式

style1 {
	background-color: #ffffff;
	&:hover {
		background-color: #000000;
	}
}
```



##### 嵌套属性

```scss
body {
	font-family: 'fangsong';
	font-size: 20px;
	font-weight: 700
}

//使用嵌套属性后，属性根可以提取出来
body {
   font: {
        family: 'fangsong';
        size: 20px;
        weight: 700;
	} 
}

```



##### 混合-Mixins

**用名字定义好的样式**

```scss
@mixin 名字（参数1，参数2，...）
{
........样式.......

}

//下面定义了一个名字为hunhe的mixin，然后在div这个选择器里通过（@include 名字）调用 ）
@mixin hunhe {
     color: red;
     a {
         font-size: 12px;
     }
}

div{
    @include hunhe;  
}

//上面的用法相当于
div {
  color: red;
}
div a {
  font-size: 12px;
}
```



##### Mixins传参

```scss
@mixin hunhe($one, $two) {
     color: $one;
     a {
         color: $one;
         font-size: $two;
     }
}

div{
    @include hunhe(red, 15px);  
}

//div也可以这样写,指定参数名，参数位置就可以随意变换
div{
    @include hunhe($two:15px, $one:red);  
}
```



##### 继承/扩展

**一个选择器可以继承另一个选择器的全部样式**

**two类里继承了.one类的全部样式 （@extend 名字）； *还不止.one的，跟.one相关的都继承了*** 

```scss
.one{
    color: #000;
}
.one a{
    font-size: 10px;
}
.two{
    @extend .one;
    background-color: #fff;
}

//上述写法相当于以下样式
.one, .two {
  color: #000;
}

.one a, .two a {
  font-size: 10px;
}

.two {
  background-color: #fff;
}
```



##### Partials与@import

**@import 引入一个.scss后缀的文件作为自己的一部分，被引入的那个文件并不会转换成.css格式的，所以此文件命名要注意以下划线开头，如：_base.scss ，引入它的时候不用写下划线。****

**引入语法：@import: “…路径”;**

```scss
.one{
    color: #000;
}
.one a{
    font-size: 10px;
}
.two{
    @extend .one;
    background-color: #fff;
}

//上述写法相当于以下样式
.one, .two {
  color: #000;
}

.one a, .two a {
  font-size: 10px;
}

.two {
  background-color: #fff;
}
```



##### hsl与hsla

**色相，饱和度，明度，不透明度**

```scss
body{   
   background-color: hsl(5, 20%, 20%,0.5);
} 

//相当于

body {
  background-color: rgba(61, 43, 41, 0.5);
}
```



##### **lighten**与**darken**

**lighten让颜色更亮，darken让颜色更暗**

**使用方法：lighten（颜色，增加亮度的百分比）**

```scss
body{   
   background-color: lighten(rgb(228, 145, 145),50%);
   color: darken(rgb(228, 145, 145),50%);
} 

//相当于

body {
  background-color: white;
  color: #5f1717;
}
```



##### **saturate**与**desaturate**

**用来调整颜色纯度，saturate让颜色更纯 ，desaturate让颜色不纯**

**使用方法：saturate（颜色，百分比）**

```scss
$base-color: hsl(221, 50%, 50%);
$saturate-color: saturate($base-color, 50%);
$desaturate-color: desaturate($base-color, 30%);
```



##### opacity**与**transparentize**

**opacity用来增加颜色透明度 ，transparentize用来降低颜色的透明度**

**使用方法：saturate（颜色，百分比）** 

```scss
$base-color: hsla(221, 50%, 50%， 0.5);
$fade-in-color: opacity($base-color, 0.3);
$fade-out-color: transparentize($base-color, 0.2);

.alert {
    background-color: $fade-in-color;
    border: 1px solid $fade-out-color;
}

//相当于
.alert {
    background-color: rgba(0, 76, 255, 0.8);
    border: 1px solid rgba(0, 76, 255, 0.3);
}
```



##### **Interpolation** 

**把一个值插入到另一个值，具体用法如 #{变量}** 

```scss
$yanse: color;
body{   
   #{$yanse}: red;
} 

//相当于
body {
  color: red;
}
```



##### @if 

```scss
@if 判断条件 {
.......执行语句...
} @else if 判断条件{
  .......执行语句...
}
 @else {
  ...else有就写没就不写....
}

//举例说明
$jia: false;
body {   
   @if false{
       color: red;
   }
   @if 2>3 {
       background-color: white;
   }@else{
       background-color: black;
   }  
} 

//相当于
body {
  background-color: black;
}
```



##### @for

```scss
结束值不执行：
@for 变量 from 开始值 to 结束值 {
     ......
}
结束值也执行：
@for 变量 from 开始值 through 结束值 {
     ......
}

//举例说明
@for $i from 1 to 3 {    
    .div#{$i}{
       height: $i*20px;
    }
}

//相当于
.div1 {
  height: 20px;
}

.div2 {
  height: 40px;
}
```



##### @each

**能循环一遍列表的值，列表相当于数组**

```scss
@each 变量 in 列表{
	...
}

//举例说明
$yanse: red blue black;
@each $i in $yanse {  
    .div-#{$i}{
      color: $i;
    }
}

//相当于
.div-red {
  color: red;
}

.div-blue {
  color: blue;
}

.div-black {
  color: black;
}
```



##### @while

**有判断条件更灵活**

```scss
@while 条件 {
   ...
}

//举例说明
$gao: 1;
@while $gao<4 {
    .div#{$gao}{
        height: $gao*10px;
    }
   $gao : $gao+1;
}

//相当于
.div1 {
  height: 10px;
}

.div2 {
  height: 20px;
}

.div3 {
  height: 30px;
}
```



##### @function

**自定义函数**

```scss
@function 名字(参数1，参数2，..){
	....
}

//举例说明
@function ziji ($bian)
{
    @return $bian+10px;
}

div{
    width: ziji(5px);
}

//相当于
div {
  width: 15px;
}
```



##### ！default

**可以在变量的结尾添加！default给一个未通过！default声明赋值的变量赋值，如果变量已经被赋值，不会再被重新赋值，但是如果变量还没有被赋值，则会被赋予新的值。注意，如果变量是null空值时则视为未被！default赋值。**

```scss
$content: "First content";
$content: "Second content?" !default;

#main {
    content: $content;
}

//相当于
#main {
    content: "First content";
}
```



##### ！global

**变量支持块级作用域，嵌套规则内定义的变量只能在嵌套规则内使用的（局部变量），不在嵌套规则定义的变量则可在任何地方使用（全局变量）。将局部变量转换为全局变量可以添加！global声明**

```scss
#foo {
    $width: 5em !global;
    width: $width;
}

#bar {
    width: $width;
}
```



##### 三元运算符

表达式： if(expression, value, value2)

```scss
p {
    color: if(1 + 1 == 2, green, yellow);
}

//相当于
p {
    color: green;
}
```


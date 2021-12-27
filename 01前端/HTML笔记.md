HTML笔记

------

◆HTML不区分大小写。

◆注释HTML语句时，把光标放在目标行，按下Ctrl+/键。再次使用即取消。

◆在HTML中使用<!--注释语句-->。在CSS中使用/*     */注释。

------



```html
<!DOCTYPE html>  让浏览器得知自己要处理的内容是HTML
<html lang="en"> 文档中HTML部分的开始
<head></head>  提供有关文档内容和构建信息的
```

```html
<a href="目标网址" title="鼠标滑过显示的文本">链接显示的文本</a>
<!-- 会在新窗口打开链接页面 -->
<a href="目标网址" target="_blank">链接显示的文本</a>
```

```html
<img src="图片地址" alt="下载失败时的替换文本" title="鼠标滑过图片时显示的文本">
```

```html
<form>
  姓名：<input type="text" name="myName"> <br/>
  密码：<input type="password" name="pass">
</form>
```

```html
<input   type="radio/checkbox"   value="值"    name="名称"   checked="checked"/>
<!--
	当 type="radio" 时，控件为单选框，当 type="checkbox" 时，控件为复选框。
	value：提交数据到服务器的值（后台程序PHP使用）。
	name：为控件命名，以备后台程序 ASP、PHP 使用。
	checked：当设置 checked="checked" 时，该选项被默认选中。
	注意:同一组的单选按钮，name 取值一定要一致，这样同一组的单选按钮才可以起到单选的作用。	
-->
```



#### 元素分类

------

##### 行内元素

◆a、b、span、img、input、strong、select、label、em、button、textarea;

##### 块级元素

◆div、ul、li、dl、dt、dd、p、h1-h6、blockquote;

##### 空元素

◆即没有内容的HTML元素，例如：br、meta、hr、link、input、img;



------

#### 字体格式设置

◆用<code>加一段编程代码，用<pre>加很多段代码;

◆<em>的内容在浏览中显示为斜体;

◆<strong>显示为加粗，<b>也可以用来设置粗体;

◆<u></u>表示下划线;





------

#### Doctype

Doctype声明于文档最前面，告诉浏览器以何种方式来渲染页面，这里有两种模式，严格模式和混杂模式。

严格模式的排版和JS 运作模式是 以该浏览器支持的最高标准运行。

混杂模式，向后兼容，模拟老式浏览器，防止浏览器无法兼容页面。

**用法：**

<!DOCTYPE> 声明必须是 HTML 文档的第一行，位于 <html> 标签之前。

<!DOCTYPE> 声明不是 HTML 标签；它是指示 web 浏览器关于页面使用哪个 HTML 版本进行编写的指令。

在 HTML 4.01 中，<!DOCTYPE> 声明引用 DTD，因为 HTML 4.01 基于 SGML。DTD 规定了标记语言的规则，这样浏览器才能正确地呈现内容。

HTML5 不基于 SGML，所以不需要引用 DTD。

**常用的 DOCTYPE 声明：**

```html
<!-- html5 -->
<!DOCTYPE html>

<!-- HTML 4.01 Strict -->
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">

<!-- HTML 4.01 Transitional -->
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">

<!--HTML 4.01 Frameset -->
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Frameset//EN" "http://www.w3.org/TR/html4/frameset.dtd">

<!-- XHTML 1.0 Strict -->
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
```



------

#### iframe

**定义：**iframe 用于在页面内显示页面，使用 <iframe> 会创建包含另外一个文档的内联框架（即行内框架）

iframe就是我们常用的iframe标签：<iframe>。iframe标签是框架的一种形式，也比较常用到，iframe一般用来包含别的页面，例如我们可以在我们自己的网站页面加载别人网站或者本站其他页面的内容。iframe标签的最大作用就是让页面变得美观。iframe标签的用法有很多，主要区别在于对iframe标签定义的形式不同，例如定义iframe的长宽高。

![](前端图片/1-1F31220532c23.png)

```html
<iframe src="https://www.baidu.com" height="400" width="700" name="demo" frameborder="0" scrolling="auto" sandbox="allow-same-origin allow-top-navigation allow-forms allow-scripts"  ></iframe>
```

划重点：
 1.sandbox="allow-same-origin allow-top-navigation allow-forms allow-scripts"
 这个参数是必须要加的，否则出来的界面是空白一片。
 2.如果想要无边框的，清新自然的感觉，那么加上frameborder="0"

**iframe 的常用属性：**

```
1、width		定义 iframe 的宽度
2、height	定义 iframe 的高度
3、name		规定 iframe 的名称
4、frameborder	规定是否显示边框，值为 0（不显示）和 1（显示）
5、scrolling		规定是否在 iframe 中显示滚动条，值为 yes、no、auto
6、src		设置 iframe 的地址（页面/图片）
7、srcdoc	用来替换 iframe 中 html、body 里的内容（ IE 不支持）
8、sandbox	对 iframe 进行内容限制，值为：
allow-forms
allow-same-origin
allow-scripts
allow-top-navigation
...
支持 IE10+
```

**用处：**

**优点：**

重载页面时不需要整个页面进行重载，只需要重载一个框架页，减少数据传输，增加网页加载速度

**缺点：**

会阻塞主页面的onload事件。window 的 onload 事件需要在所有 iframe 加载完毕后（包含里面的元素）才会触发。在 Safari 和 Chrome 里，通过 JavaScript 动态设置 iframe 的 SRC 可以避免这种阻塞情况。

搜索引擎无法解读这种页面，不利于SEO

iframe和主页面共享连接池，而浏览器对相同区域有限制所以会影响性能。浏览器只能开少量的连接到 web 服务器。这意味着 iframe 在加载资源时可能用光了所有的可用连接，从而阻塞了主页面资源的加载。一种解决办法是，在主页面上重要的元素加载完毕后，再动态设置 iframe 的 SRC。



------

#### meta标签

```
meta是html文档头部的一个标签，这个标签对用户不可见，是给搜索引擎看的。
<meta charset="UTF-8"> 使用的编码格式，大部分是utf-8。
meta标签属性用法分成两大类：
```

![](前端图片/2112309-20210111113611511-397371797.png)



#### 表格

##### 创建表格的五个元素：table、tbody、th、tr、td

```html
<body>
    <table border="1px">
        <thead>
            <tr>
                <th>用户名</th>         <!--表头-->
                <th>性别</th>
                <th>密码</th>
            </tr>
        </thead>

        <tbody>
            <tr>
                <td>Admin</td>
                <td>男</td>
                <td>123</td>
            </tr>
            <tr>
                <td>赵凯</td>
                <td>男</td>
                <td>233</td>
            </tr>
        </tbody>

        <tfoot>
            <td>用户名</th>        
            <td>性别</th>
            <td>密码</th>
        </tfoot>
    </table>
</body>
```

##### 合并行单元格和列单元格

```html
<body>
<table border="1px">
    <thead>
    <tr>
        <th rowsapn="2">AAA</th>         <!--合并两个列单元格-->
        <th>BBB</th>
        <th>CCC</th>
        <th>DDD</th>
    </tr>

    <tr>
    	<!--  <td>111</td>  -->					<!--合并两个列单元格要将此框删除-->
        <td colspan="2">222</td>			
        <!--   <td>333</td>   -->				<!--合并两个行单元格要将此框删除-->
        <td>444</td>
    </tr>
    <tr>
    	<td>555</td>
        <td>666</td>
        <td>777</td>
        <td>888</td>        
    </tr>

</table>
</body>
```



------

#### 排序标签

##### 有序标签ol

```html
<body>
    <ol>
        <li>a</li>		<!-- 默认按数据123排序输出 -->
        <li>a</li>
        <li>a</li>
    </ol>

    <ol type="a">		<!-- 用a小写字母进行排序，还有类似的大写字母和大小写罗马数字 -->
        <li>a</li>    
        <li>a</li>
        <li>a</li>
    </ol>

    <ol type="reversed">		<!-- 反序输出 -->
        <li>a</li>    
        <li>a</li>
        <li>a</li>
    </ol>

    <ol>
        <li>A</li>		<!-- 嵌套排序 -->
        <ol type="a">
            <li>a</li>
            <li>a</li>  
        </ol>    
    </ol>
</body>
```

##### 无序标签ul

```html
<body>
    <ul>
        <li>a</li>		<!-- 标签全部为黑色的小圆点，没有顺序 -->
        <li>a</li>
        <li>a</li>
    </ul>
</body>
```

------

#### 表单

```html
<form>
    <input type="text">		<!-- 单行文本 -->
    <br><br>
    <input type="text" value="靠谱学院">		<!-- 占位符 -->
    <br><br>    
    <input type="text" placeholder="靠谱学院">		<!-- 不占文本框内的 -->
    <br><br>    
    <input type="text" placeholder="maxlength" maxlength="8">		<!-- 最大输入字符数量 -->
    <br><br>    
    <input type="text" placeholder="靠谱学院" size="50">		<!-- 拓宽单行文本框 -->
    <br><br>    
    <input type="text" value="靠谱学院" readonly>		<!-- 只读 -->
    <br><br>
    
    <!-- 设置文本框的长宽度 -->
    <textarea row="20" cols="40">aaaaaaaaaaaaaaaaaaaaaaaaa</textarea>
</form>
```



##### 三种按钮

```html
<form>
    <input type=button value="按键">
    <button>按键</button>			<!-- js合作并且作为绑定事件 -->
    <input type="submit" value="提交">			<!-- 提交表单，适用范围比input button小一些 -->
</form>
```

```html
<form>
    <input type="range" min="-100" max="500" step="100">		<!-- 数字滑动 -->
    
    <!-- value代表初始位置 -->
    <input type="range" min="-100" max="500" step="100" value="-100"> 	
    
    <input type="number" min="-100" max="500" value="0">		<!-- 手动输入数字 -->
</form>
```



##### 复选框

```html
<form>
    <input type="checkbox">选择
</form>
```



##### 点选框

```html
<form>
    <input type="radio" name="a" checked>星月
	<input type="radio" name="a">星月
	<input type="radio" name="a">星月
</form>
```



##### 弹选框

```html
<form>
    <select>
        <option>苹果</option>
        <option>香蕉</option>
        <option>西瓜</option>
    </select>
</form>
```



##### 可添加选择项的弹选框

```html
<form>
    <input type="text" list="datalist1">
    <datalist id="datalist1">
        <option>苹果</option>
        <option>香蕉</option>
        <option>西瓜</option>    	
    </datalist>
</form>
```



##### 设置提交框格式

```html
<input type="email">
<input type="tel">
<input type="url">
<input type="date">获取时间
<input type="color">获取颜色
<input type="hidden" value="123">隐藏文本框
<input type="image" src="Download.png" width="80px">图片按钮

<!-- 还可以设置属性multiple，可以上传多个文件；设置属性为required，则必须上传一个文件 -->
<input type="file" multiple>上传文件    

<!-- 当使用input元素上传文件提交表单时，要设置如下内容 -->
<form enctype="multipart/form-data">
</form>
```



##### 创建分区响应图

```html
<!-- alt表示图片未加载时显示的文字 -->
<img src="Download.png" width="128px" alt="下载按键">


<!-- 设置方形点击区域 -->
<img src="time.png" usemap="#map1">
<form>
    <input type="image" src="time.jpg">
</form>
<map name="map1">
    <!-- coords四个整数分别代表图像左上右下四个边缘 -->
	<area href="time.html" shape="rect" coords="38,63,175,200" target="_blank">
 	<area href="weather.html" shape="rect" coords="38,63,175,200" target="_blank">   
</map>


<!-- 设置圆形点击区域 -->
<img src="Download.png" width="128" usemap="#map2">
<map name="map2">
    <!-- coords三个整数分别代表图像左边缘和右边缘到圆心的距离以及圆的半径 -->
	<area href="xxx.html" shape="circle" coords="64px,64px,64px" target="_blank">
</map>
<a target="_blank" href="xxx.html">
<img src="Download.png" width="128">
</a>
```



##### 设置视频播放

```html
<!-- controls是显示控制图标，preload是设置为视频预加载，改为none则为不加载，poster是设置视频封面图片 -->
<video src="xxx.mp4" height="500px" controls preload="metadata" poster="123.png">
	<source src="xxx.mp4" type="video/mp4">
    <source src="xxx.ogv" type="video/ogg">
</video>
```



#### HTML语义化

**1、什么是HTML语义化？**

基本上都是围绕着几个主要的标签，像标题（H1~H6）、列表（li）、强调（strong em）等等。

根据内容的结构化（内容语义化），选择合适的标签（代码语义化）便于开发者阅读和写出更优雅的代码的同时让浏览器的爬虫和机器很好地解析。

**2、为什么要语义化？**

- 为了在没有CSS的情况下，页面也能呈现出很好地内容结构、代码结构；
- 用户体验：例如title、alt用于解释名词或解释图片信息、label标签的活用；
- 有利于[SEO](http://baike.baidu.com/view/1047.htm)（搜索引擎优化）：和搜索引擎建立良好沟通，有助于爬虫抓取更多的有效信息：[爬虫](http://baike.baidu.com/view/998403.htm)依赖于标签来确定上下文和各个关键字的权重；
- 方便其他设备解析（如屏幕阅读器、盲人阅读器、移动设备）以意义的方式来渲染网页；
- 便于团队开发和维护，语义化更具可读性，是下一步吧网页的重要动向，遵循W3C标准的团队都遵循这个标准，可以减少差异化。

**3、写HTML代码时应注意什么？**

- 尽可能少的使用无语义的标签div和span；
- 在语义不明显时，既可以使用div或者p时，尽量用p, 因为p在默认情况下有上下间距，对兼容特殊终端有利；
- 不要使用纯样式标签，如：b、font、u等，改用css设置。
- 需要强调的文本，可以包含在strong或者em标签中（浏览器预设样式，能用CSS指定就不用他们），strong默认样式是加粗（不要用b），em是斜体（不用i）；
- 使用表格时，标题要用caption，表头用thead，主体部分用tbody包围，尾部用tfoot包围。表头和一般单元格要区分开，表头用th，单元格用td；
- 表单域要用fieldset标签包起来，并用legend标签说明表单的用途；
- 每个input标签对应的说明文本都需要使用label标签，并且通过为input设置id属性，在lable标签中设置for=someld来让说明文本和相对应的input关联起来。

 **4、HTML5新增了哪些语义标签**

在HTML 5出来之前，我们用`div`来表示页面章节，但是这些`div`都没有实际意义。（即使我们用css样式的id和class形容这块内容的意义）。这些标签只是我们提供给浏览器的指令，只是定义一个网页的某些部分。但现在，那些之前没“意义”的标签因为html5的出现消失了，这就是我们平时说的“语义”。



#### **HTML5元素标签**

首先html5为了更好的实践web语义化，增加了header，footer，nav,aside,section等语义化标签，在表单方面，为了增强表单，为input增加了color，emial,data ,range等类型，在存储方面，提供了sessionStorage，localStorage和离线存储，通过这些存储方式方便数据在客户端的存储和获取，在多媒体方面规定了音频和视频元素audio和video，另外还有地理定位，canvas画布，拖放，多线程编程的web worker和websocket协议。

HTML5节元素标签包括`body article nav aside section header footer hgroup `，还有`h1-h6 address`。

- `address`代表区块容器，必须是作为联系信息出现，邮编地址、邮件地址等等,一般出现在footer。
- `h1-h6`因为hgroup，section和article的出现，h1-h6定义也发生了变化，允许一张页面出现多个h1。

**html5的布局**

但是也不要因为html5新标签的出现，而随意用之，错误的使用肯定会事与愿违。所以有些地方还是要用div的，就是因为div没有任何意义的元素，他只是一个标签，仅仅是用来构建外观和结构。因此是最适合做容器的标签。

结论：不能因为有了HTML 5标签就弃用了div，每个事物都有它的独有作用的。

节点元素标签因使用的地方不同，我将他们分为：节元素标签、文本元素标签、分组元素标签分开来讲解HTML5中新增加的语义化标签和使用总结。

**header元素**

header 元素代表“网页”或“section”的页眉。
通常包含`h1-h6`元素或`hgroup`，作为整个页面或者一个内容块的标题。也可以包裹一节的目录部分，一个搜索框，一个`nav`，或者任何相关logo。

**footer元素**

`footer`元素代表“网页”或“section”的页脚，通常含有该节的一些基本信息，譬如：作者，相关文档链接，版权资料。如果`footer`元素包含了整个节，那么它们就代表附录，索引，提拔，许可协议，标签，类别等一些其他类似信息。

**hgroup元素**

`hgroup`元素代表“网页”或“section”的标题，当元素有多个层级时，该元素可以将`h1`到`h6`元素放在其内，譬如文章的主标题和副标题的组合

hgroup使用注意：

- 如果只需要一个h1-h6标签就不用hgroup
- 如果有连续多个h1-h6标签就用hgroup
- 如果有连续多个标题和其他文章数据，h1-h6标签就用hgroup包住，和其他文章元数据一起放入header标签



#### 浏览器渲染引擎

**一个渲染引擎主要包括**：`HTML解析器`，`CSS解析器`，`javascript引擎`，`布局layout模块`，`绘图模块`

**HTML解析器**：解释HTML文档的解析器，主要作用是将HTML文本解释成DOM树。

**CSS解析器**：它的作用是为DOM中的各个元素对象计算出样式信息，为布局提供基础设施

**Javascript引擎**：使用Javascript代码可以修改网页的内容，也能修改css的信息，javascript引擎能够解释javascript代码，并通过DOM接口和CSS树接口来修改网页内容和样式信息，从而改变渲染的结果。

**布局（layout）**：在DOM创建之后，Webkit需要将其中的元素对象同样式信息结合起来，计算他们的大小位置等布局信息，形成一个能表达这所有信息的内部表示模型

**绘图模块（paint）**：使用图形库将布局计算后的各个网页的节点绘制成图像结果

##### 渲染过程

![](前端图片/20201005103415270.png)

1.遇见 HTML 标记，调用HTML解析器解析为对应的 token （一个token就是一个标签文本的序列化）并构建 DOM 树（就是一块内存，保存着tokens，建立它们之间的关系）。

2.遇见 style/link 标记 调用（可能是 html/css 解析器）解析器 处理 CSS 标记并构建 CSS样式树。

3.遇见 script 标记 调用 javascript解析器 处理script标记，绑定事件、修改DOM树/CSS树 等

4.将 DOM树 与 CSS树 合并成一个render 树（渲染树）。

5.根据渲染树来渲染，以计算每个节点的几何信息（这一过程需要依赖图形库）。

6.将各个节点绘制到屏幕上。

`总结：`**真正渲染到页面，一定是发生在DOM-Tree和CSSOM树都已经构建完成时，所以HTML和CSS都是阻碍页面渲染的东西**

##### CSS阻塞

 声明：只有link引入的外部css才能够产生阻塞。

1.style标签中的样式：

 (1). 由html解析器进行解析；

 (2). 不阻塞浏览器渲染（可能会产生“闪屏现象”）；

 (3). 不阻塞DOM解析；

2.link引入的外部css样式（推荐使用的方式）：

(1). 由CSS解析器进行解析。

(2). 阻塞浏览器渲染(可以利用这种阻塞避免“闪屏现象”)。

(3). 阻塞其后面的js语句的执行：

(4). 不阻塞DOM的解析：

优化核心理念：

尽可能快的提高外部css加载速度

(1).使用CDN节点进行外部资源加速。

(2).对css进行压缩(利用打包工具，比如webpack,gulp等)。

(3).减少http请求数，将多个css文件合并。

(4).优化样式表的代码（避免出现太多级的选择器）

##### JS阻塞

 1.阻塞DOM解析:

原因：浏览器不知道后续脚本的内容，如果先去解析了下面的DOM，而随后的js删除了后面所有的DOM，那么浏览器就做了无用功，浏览器无法预估脚本里面

体做了什么操作，例如像document.write这种操作，索性全部停住，等脚本执行完了，浏览器再继续向下解析DOM。

2.阻塞页面渲染:

原因：js中也可以给DOM设置样式，浏览器同样等该脚本执行完毕，再继续干活，避免做无用功。

3.阻塞后续js的执行:

原因：维护依赖关系，例如：必须先引入jQuery再引入bootstrap。

**补充**

1.css的解析和js的执行是互斥的（互相排斥），css解析的时候js停止执行，js执行的时候css停止解析。

2.无论css阻塞，还是js阻塞，都不会阻塞浏览器加载外部资源（图片、视频、样式、脚本等）

原因：浏览器始终处于一种：“先把请求发出去”的工作模式，只要是涉及到网络请求的内容，无论是：图片、样式、脚本，都会先发送请求去获取资源，至于资

到本地之后什么时候用，由浏览器自己协调。这种做法效率很高。

3.WebKit 和 Firefox 都进行了【预解析】这项优化。在执行js脚本时，浏览器的其他线程会解析文档的其余部分，找出并加载需要通过网络加载的其他资源。通

过这种方式，资源可以在并行连接上加载，从而提高总体速度。请注意，预解析器不会修改 DOM 树。




#### href、src区别

href是Hypertext Reference的缩写，表示超文本引用。用来建立当前元素和文档之间的链接。常用的有：link、a。例如：

```html
<link href="reset.css" rel="stylesheet"/>
```

浏览器会识别该文档为css文档，并行下载该文档，并且不会停止对当前文档的处理。这也是建议使用link，而不采用@import加载css的原因。
src是source的缩写，src的内容是页面必不可少的一部分，是引入。src指向的内容会嵌入到文档中当前标签所在的位置。常用的有：img、script、iframe。例如:

```html
<script src="script.js"></script>
```

当浏览器解析到该元素时，会暂停浏览器的渲染，知道该资源加载完毕。这也是将js脚本放在底部而不是头部的原因，最好还是放在 body 尾部。

简而言之，src用于替换当前元素；href用于在当前文档和引用资源之间建立联系。

css下载完会构建cssom，js由于可能会改变cssom所以必须等待cssom构建后才开始parse。



#### link标签与import标签区别

link属于html标签，而@import是css提供的

页面被加载时，link会同时被加载，而@import引用的css会等到页面加载结束后加载。

link是html标签，因此没有兼容性，而@import只有IE5以上才能识别。

link方式样式的权重高于@import的。

### jQuery

jQuery是一款优秀的JavaScript库，使用jQuery能让我们对HTML文档遍历和操作、事件处理、动画以及Ajax变得更加简单。

```html
<head>
    <meta charset="UTF-8">
    <title>jQuery-HelloWorld</title>
    <script src="js/jQuery-1.12.4.js"></script>
    <script>
        //1、原生JS的固定写法
    	window.onload=function(ev){}
        
        //2、jQuery的固定写法
        $(document).ready(function(){
                          alert("hello lnj");
                          })
    </script>
</head>
```



##### jQuery与JS入口函数的区别

原生JS和jQuery入口函数的加载模式不同。

原生JS会等到DOM元素加载完毕，并且图片也加载完毕都会执行。

jQuery会等到DOM元素加载完毕，但不会等到图片也加载完毕就会执行。

```html
<head>
    <meta charset="UTF-8">
    <title>jQuery与JS入口函数的区别</title>
    <script src="js/jQuery-1.12.4.js"></script>
    <script>
        window.onload=function(ev){
            //1、通过原生的JS入口函数可以拿到DOM元素
            var img=document.getElementsByTagName("img")[0];
            console.log(img);
            
            //2、通过原生的JS入口函数可以拿到DOM元素的宽高
            var width=window.getComputedStyle(img).width;
            console.log("onload",width);
        }
             
        $(document).ready(function(){
            //1、通过jQuery入口函数可以拿到DOM元素
            var $img=$("img");
            console.log($img);
            
            //2、通过jQuery入口函数不可以拿到DOM元素的宽高
            var $width=$img.width();
            console.log("ready",$width);
        })
        
    </script>
</head> 

<body>
    <img src="图片网址">
</body>
```

```html
<head>
    <meta charset="UTF-8">
    <title>jQuery与JS入口函数的区别</title>
    <script src="js/jQuery-1.12.4.js"></script>
    <script>
        
        //1、原生的JS如果编写了多个入口函数，后面编写的会覆盖前面编写的
        //2、jQuery中编写多个入口函数，后面的不会覆盖前面的
		window.onload=function(ev){
            alert("hello lnj1");
        }
		window.onload=function(ev){
            alert("hello lnj2");
        }        
    
        $(document).ready(function(){
            alert("hello lnj1");
        })
        $(document).ready(function(){
            alert("hello lnj2");
        })        
    </script>
</head> 
```



##### jQuery入口函数的其它写法

```html
<head>
    <meta charset="UTF-8">
    <title>jQuery入口函数的其它写法</title>
    <script src="js/jQuery-1.12.4.js"></script>
    <script>
		//第一种写法
        $(document).ready(function(){
            alert("hello lnj");
        })
        
		//第二种写法
        jQuery(document).ready(function(){
            alert("hello lnj");
        })
        
		//第三种写法（推荐）
        $(function(){
            alert("hello lnj");
        })
        
		//第四种写法
        jQuery(function(){
            alert("hello lnj");
        })
    </script>
</head> 
```



##### jQuery的冲突问题

```html
<head>
    <meta charset="UTF-8">
    <title>jQuery的冲突问题</title>
    <script src="js/jQuery-1.12.4.js"></script>
    <script src="js/test.js"></script>               //假设此文件中也有$的定义
    <script>
		//1、释放$的使用权
        //注意点：释放操作必须在编写其它jQuery代码之前编写，释放之后就不能再使用$，改用jQuery
        jQuery.noConflict();
        jQuery(function(){
            alert("hello lnj");
        }
        
        //2、自定义一个访问符号
        var nj=jQuery.noConflict();
        nj(function(){
            alert("hello lnj");
        })
    </script>
</head> 
```



##### jQuery的核心函数

```html
<head>
    <meta charset="UTF-8">
    <title>jQuery的核心函数</title>
    <script src="js/jQuery-1.12.4.js"></script>               
    <script>
		//$():就代表调用jQuery的核心函数
        
        //1、接收一个函数
        $(function(){
            alert("hello lnj");
            //2、接收一个字符串
            //2.1 接收一个字符串选择器
            //返回一个jQuery对象，对象中保存了找到的DOM元素
            var $box1=$(".box1");
            var $box2=$("#box2");
            console.log($box1);
            console.log($box2);
            
            //2.2接收一个字符串代码片段
            //返回一个jQuery对象，对象中保存了创建的DOM对象
            var $p=$("<p>我是段落</p>");
            console.log($p);
            $box1.append($p);
            
            //3、接收一个DOM元素
            //会包装成一个jQuery对象返回给我们
            var span=document.getElementsByTagName("span")[0];
            console.log(span);            
            var $span=$(span);
            console.log($span);
        })
    </script>
</head> 

<body>
    <div class="box1"></div>
    <div id="box2"></div>
</body>
```



##### jQuery对象

```html
<head>
    <meta charset="UTF-8">
    <title>jQuery对象</title>
    <script src="js/jQuery-1.12.4.js"></script>               
    <script>
		$(function(){
            //1、什么是jQuery对象
            //jQuery对象是一个伪数组
            
            //2、什么是伪数组
            //有0到length-1的属性，并且有length的属性
            
            var $div=$("div");
            console.log($div);                    
        })
    </script>
</head> 

<body>
    <div>div1</div>
    <div>div2</div>
    <div>div3</div>
</body>
```



##### 静态方法与实例方法

```html
<head>
    <meta charset="UTF-8">
    <title>静态方法与实例方法</title>
    <script src="js/jQuery-1.12.4.js"></script>               
    <script>
        //1、定义一个类
		function AClass(){}
        
        //2、给这个类添加一个静态方法，直接添加给类的就是静态方法
        AClass.staticMethod=function(){
            alert("staticMethod");
        }
        //静态方法通过类名调用
        AClass.staticMethod();
        
        //3、给这个类添加一个实例方法
        AClass.prototype.instanceMethod=function(){
            alert("instanceMethod");
        }
        //实例方法通过类的实例调用
        //创建一个实例（创建一个对象)
        var a=new AClass();
        //通过实例调用实例方法
        a.instanceMethod();
    </script>
</head> 
```



##### jQuery的each方法

```html
<head>
    <meta charset="UTF-8">
    <title>jQuery的each方法</title>
    <script src="js/jQuery-1.12.4.js"></script>               
    <script>
        var arr=[1,3,5,7,9];
        var obj={0:1,1:3,2:5,3:7,4:9,length:5};
        /*
        第一个参数：遍历到的元素
        第二个参数：当前遍历到的索引
        注意点：原生的forEach方法只能遍历数组，不能遍历伪数组，会报错
        */
        arr.forEach(function(value,index){
            console.log(index,value);
        })                   
        
		//1、利用jQuery的each静态方法遍历数组
        /*
        第一个参数：当前遍历到的索引
        第二个参数：遍历到的元素
        注意点：jQuery的each方法是可以遍历伪数组的
        */
        $.each(arr,function(index.value){
            console.log(index,value);
        })
        $.each(obj,function(index,value){
            console.log(index,value);
        })
    </script>
</head> 
```



##### jQuery的map方法

```html
<head>
    <meta charset="UTF-8">
    <title>jQuery的each方法</title>
    <script src="js/jQuery-1.12.4.js"></script>               
    <script>
        var arr=[1,3,5,7,9];
        var obj={0:1,1:3,2：5，3：7，4：9，length:5};

        //利用原生JS的map方法遍历
        /*
        第一个参数：当前遍历到的元素
        第二个参数：当前遍历的索引
        第三个参数：当前被遍历的数组
        注意点：和原生的forEach一样，不能遍历伪数组
        */
        arr.map(function(value,index,array){
            console.log(index,value,array);
        })
        
        /*
        第一个参数：要遍历的数组
        第二个参数：每遍历一个元素之后执行的回调函数
        回调函数的参数：
       		第一个参数：遍历到的元素
       		第二个参数：遍历到的索引
       	注意点：和jQuery的each静态方法一样，map静态方法也可以遍历伪数组
       	*/
        
        $.map(arr,function(value,index){
            console.log(index,value);
        })
        var res=$.map(obj,function(value,index){
            console.log(index,value);
        })
        
        var res2=$.each(obj,function(index,value){
            console.log(index,value);
            return value+index;
        })
        /*
        jQuery中的each静态方法和map静态方法的区别：
        each静态方法默认的返回值就是，遍历谁就返回谁
        map静态方法默认的返回值是一个空数组
        
        each静态方法不支持在回调函数中对遍历的数组进行处理
        map静态方法可以在回调函数中通过return对遍历的数组进行处理，然后生成一个新的数组返回
        */
        console.log(res);
        console.log(res2);
    </script>
</head> 
```



##### jQuery的其它方法

```html
<head>
    <meta charset="UTF-8">
    <title>jQuery的其它方法</title>
    <script src="js/jQuery-1.12.4.js"></script>               
    <script>
        //$.trim()方法用来去除字符串两端的空格，返回值为去除空格之后的字符串
		var str="   lnj   ";
        var res=$.trim(str);
        console.log("---"+str+"---");
        console.log("---"+res+"---");
        
        //$.isWindow()方法用来判断传入的对象是windwo对象，返回true或false
        //真数组
        var arr=[1,3,5,7,9];
        //伪数组
        var arrlike={0:1,1:3,2:5,3:7,4:9,length:5};
        //对象
        var obj={"name":"lnj",age:"33"};
        //函数
        var fn=function(){};
        //window对象
        var w=window;
        var res=$.isArray(arr);
        console.log(res);
        
        //$.isArray()方法用来判断传入的对象是真数组，返回true或false
        var res=$isArray(arr);
        console.log(res);
 
        //$.isFunction()方法用来判断传入的对象是函数，返回true或false
       //jQuery本质也是一个函数
        var res=$isFunction(jQuery);
        console.log(res);				//返回true
    </script>
</head> 
```



##### jQuery的holdReady方法

```html
<head>
    <meta charset="UTF-8">
    <title>jQuery的holdReady方法</title>
    <script src="js/jQuery-1.12.4.js"></script>               
    <script>
        //$.holdReady(true)的作用就是暂停ready执行，如果不加则进入页面直接弹出
		$.holdReady(true);
        $(document).ready(function(){
            alert("ready");
        })
    </script>
</head> 

<body>
    <button>
        回复ready事件
    </button>
    <script>
    	var btn=document.getElementsByTagName("button")[0];
        btn.onclick=function(){
            $holdReady(false);
        }
    </script>
</body>
```



##### jQuery的内容选择器

```html
<head>
    <meta charset="UTF-8">
    <title>jQuery的内容选择器</title>
    <style>
        div{
            width:50px;
            height:100px;
            background:red;
            margin-top:5px;
        }
    </style>
    <script src="js/jQuery-1.12.4.js"></script>               
    <script>
		$(function(){
            //：contains(text)作用：找到包含指定文本内容的指定元素，不是文本完全相同，是包含 
            var $div=$("div:contains('我是div')");
            console.log($div);
            
            //:has(selector)作用：找到包含指定子元素的指定元素
            var $div=$("div:has('span')");
            console.log($div);            
            
            //:parent作用：找到有文本内容或有子元素的指定元素
           var $div=$("div:parent");
            console.log($div);
            
            //:empty作用：找到既没有文本内容也没有子元素的指定元素
            var $div=$("div:empty");
            console.log($div);
        })
    </script>
</head> 

<body>
	<div></div>
    <div>我是div</div>
    <div>我是div123</div>
    <div><sapn></sapn></div>
    <div><p></p></div>
</body>
```



##### 属性与属性节点

```html
<head>
    <meta charset="UTF-8">
    <title>属性与属性节点</title>
    <script src="js/jQuery-1.12.4.js"></script>               
    <script>
		$(function(){
            /*
            1、什么是属性？
            对象身上保存的变量就是属性
            
            2、如何操作属性？
            对象.属性名称=值;
            对象["属性名称"]=值;
            
            3、什么是属性节点？
            <span name="it666"></span>
            在编写HTML代码时，在HTML标签中添加的属性就是属性节点
            在浏览器中找到span这个DOM元素之后，发现看到的都是属性
            在attributes属性中保持的所有内容都是属性节点
            
            4、如何操作属性节点
            DOM元素.setAttribute("属性名称","值");
            DOM元素.getAttribute("属性名称");
            
            5、属性和属性节点有什么区别？
            任何对象都有属性，只有DOM对象才有属性节点。
            */
            
            var span=document.getElementsByTagName("span")[0];
            span.setAttribute("name","lnj");
            console.log(span.getAttribute("name"));
        })
    </script>
</head> 

<body>
	<span name="it666"></span>
</body>
```



##### jQuery的attr方法

```html
<head>
    <meta charset="UTF-8">
    <title>jQuery的attr方法</title>
    <script src="js/jQuery-1.12.4.js"></script>               
    <script>
		$(function(){
            /*
            1、attr()
            作用：获取或者设置属性节点的值
            可以传递一个参数，也可以传递两个参数
            如果传递一个参数，代表获取属性节点的值
            如何传递两个参数，代表设置属性节点的值
            
            注意点：
            如果是获取，无论找到多少个元素，都只会返回第一个元素指定的属性节点的值
            如果是设置，找到多少个元素就会设置多少个元素
            如果设置属性节点不存在，那么系统会自动新增
            
            2、removeAttr(name)
            删除属性节点
            
			注意点：
			会删除所有找到元素指定的属性节点
            */
            
			//console.log($("span").atrr("class"));
            //$("span").attr("class","box");
            //$("span").attr("abc","123");
            
            $("span").removeAttr("class name");     //会同时移除两种属性
        })
    </script>
</head> 

<body>
	<span class="span1" name="it666"></span>
	<span class="span2" name="lnj"></span>
</body>
```



##### jQuery的prop方法

```html
<head>
    <meta charset="UTF-8">
    <title>jQuery的prop方法</title>
    <script src="js/jQuery-1.12.4.js"></script>               
    <script>
		$(function(){
            /*
            1、prop方法
            特点和attr方法一致
            2、removeProp方法
            特点和removeAttr方法一致
            
			$("span").eq(0).prop("demo","it666");
			$("span").eq(1).prop("demo","lnj");
			console.log($("span").prop("demo"));
			
			$("span").removeProp("demo");
			
			注意点：
				prop方法不仅能够操作属性，它还能操作属性节点
            */
			//console.log($("span").prop("class"));
            
            console.log($("input").prop("checked"));		//true false
            console.log($("input").attr("checked"));		//checked undefined
            /*
            官方推荐在操作属性节点时，具有true和false两个属性的属性节点，
            如checked，selected或者disabled时，使用prop(),其它的使用attr()
            */
        })
    </script>
</head> 

<body>
	<span class="span1" name="it666"></span>
	<span class="span2" name="lnj"></span>
    
    <input type="checkbox" checked>
</body>
```



##### jQuery操作类相关的方法

```html
<head>
    <meta charset="UTF-8">
    <title>jQuery操作类相关的方法</title>
    <style>
        *{
            margin:0;
            padding:0;
        }
        .class1{
            width:100px;
            height:100px;
            background:red;
        }
        .class2{
            border:10px solid #000;
        }
    </style>
    <script src="js/jQuery-1.12.4.js"></script>               
    <script>
		$(function(){
            /*
			1、addClass()
			添加一个类，如果要添加多个，多个类名之间用空格隔开即可
			
			2、removeClass()
			删除类，如果删除多个，多个类名之间用空格隔开即可
			
			3、toggleClass()
			切换类,有该类就删除，没有该类就添加
            */
         var btns=document.getElementsByTagName("button");
            btns[0].onclick=function(){
                //$("div").addClass("class1");
                $("div").addClass("class1 class2");
            }
            btns[1].onclick=function(){
                $("div").removeClass("class2");
            }
            btns[2].onclick=function(){
                $("div").toggleClass("class1 class2");
            }
        })
    </script>
</head> 

<body>
	<button>添加类</button>
	<button>删除类</button>
	<button>切换类</button>   
    <div></div>
</body>
```



##### jQuery文本值相关的方法

```html
<head>
    <meta charset="UTF-8">
    <title>jQuery文本值相关的方法</title>
    <style>
        *{
            margin:0;
            padding:0;
        }
        div{
            width:100px;
            height:100px;
            border:1px solid #000;
        }
    </style>
    <script src="js/jQuery-1.12.4.js"></script>               
    <script>
		$(function(){
            /*
			1、html
			和原生JS中的innerHTML一模一样
			
			2、text
			和原生JS中的innerText一模一样		
            
			3、val
			和原生JS中的innerVal一模一样
            */
         var btns=document.getElementsByTagName("button");
            btns[0].onclick=function(){
				$("div").html("<p>我的段落<span>我是span</span></p>");
            }
            btns[1].onclick=function(){
				console.log($("div").html());
            }
            btns[2].onclick=function(){
				$("div").text("<p>我的段落<span>我是span</span></p>");			
            }
            btns[3].onclick=function(){
				console.log($("div").text());
            }
            btns[4].onclick=function(){
				$("input").val("请输入内容");
            }   
            btns[5].onclick=function(){
				console.log($("input").val());
            }            
        })
    </script>
</head> 

<body>
	<button>设置html</button>
	<button>获取html</button>
	<button>设置text</button>   
	<button>获取text</button>     
	<button>设置value</button>     
    <div></div>
</body>
```



##### jQuery操作CSS样式的方法

```html
<head>
    <meta charset="UTF-8">
    <title>jQuery操作CSS样式的方法</title>
    <script src="js/jQuery-1.12.4.js"></script>               
    <script>
		$(function(){
			//编写jQuery相关代码
            //1、逐个设置
            $("div").css("width","100px");
            $("div").css("height","100px");
            $("div").css("background","red");

            //2、链式设置，注意，如果链式操作大于3步，建议分开
            $("div").css("width","100px").css("height","100px").css("backgound","blue");
            
			//3、批量设置
            $("div").css({
                width:"100px",
                height:"100px",
                background："red"
            })
            
            //4、获取CSS样式值
            console.log($("div").css("width"));
        })
    </script>
</head> 

```



### Ajax

AJAX = Asynchronous JavaScript and XML（异步的 JavaScript 和 XML）。

AJAX 不是新的编程语言，而是一种使用现有标准的新方法。

AJAX 是一种在无需重新加载整个网页的情况下，能够更新部分网页的技术。



##### XHR创建对象

创建 XMLHttpRequest 对象的语法：

```html
variable=new XMLHttpRequest();
```

老版本的 Internet Explorer （IE5 和 IE6）使用 ActiveX 对象：

```html
variable=new ActiveXObject("Microsoft.XMLHTTP");
```

为了应对所有的现代浏览器，包括 IE5 和 IE6，请检查浏览器是否支持 XMLHttpRequest 对象。如果支持，则创建 XMLHttpRequest 对象。如果不支持，则创建 ActiveXObject ：

```html
var xmlhttp;
if (window.XMLHttpRequest)
  {// code for IE7+, Firefox, Chrome, Opera, Safari
  xmlhttp=new XMLHttpRequest();
  }
else
  {// code for IE6, IE5
  xmlhttp=new ActiveXObject("Microsoft.XMLHTTP");
  }
```



##### AJAX - 向服务器发送请求

XMLHttpRequest 对象用于和服务器交换数据。

如需将请求发送到服务器，我们使用 XMLHttpRequest 对象的 open() 和 send() 方法：

```html
xmlhttp.open("GET","test1.txt",true);
xmlhttp.send();
```

| 方法                         | 描述                                                         |
| ---------------------------- | ------------------------------------------------------------ |
| open(*method*,*url*,*async*) | 规定请求的类型、URL 以及是否异步处理请求。                                                           method*：请求的类型；GET 或 POST                                                                                        url*：文件在服务器上的位置                                                                                                       async：true（异步）或 false（同步） |
| send(*string*)               | 将请求发送到服务器。                                                                                                                string：仅用于 POST 请求 |

与 POST 相比，GET 更简单也更快，并且在大部分情况下都能用。

然而，在以下情况中，请使用 POST 请求：

- 无法使用缓存文件（更新服务器上的文件或数据库）
- 向服务器发送大量数据（POST 没有数据量限制）
- 发送包含未知字符的用户输入时，POST 比 GET 更稳定也更可靠



如果需要像 HTML 表单那样 POST 数据，请使用 setRequestHeader() 来添加 HTTP 头。然后在 send() 方法中规定您希望发送的数据：

| 方法                               | 描述                                                         |
| ---------------------------------- | ------------------------------------------------------------ |
| setRequestHeader(*header*,*value*) | 向请求添加 HTTP 头。                                                                                               *header*: 规定头的名称                                                                                                   *value*: 规定头的值 |

```html
xmlhttp.open("POST","ajax_test.asp",true);
xmlhttp.setRequestHeader("Content-type","application/x-www-form-urlencoded");
xmlhttp.send("fname=Bill & lname=Gates");
```



##### AJAX - 服务器响应

如需获得来自服务器的响应，请使用 XMLHttpRequest 对象的 responseText 或 responseXML 属性。

| 属性         | 描述                       |
| ------------ | -------------------------- |
| responseText | 获得字符串形式的响应数据。 |
| responseXML  | 获得 XML 形式的响应数据。  |

如果来自服务器的响应并非 XML，请使用 responseText 属性。

responseText 属性返回字符串形式的响应，因此您可以这样使用：

```html
document.getElementById("myDiv").innerHTML=xmlhttp.responseText;
```



如果来自服务器的响应是 XML，而且需要作为 XML 对象进行解析，请使用 responseXML 属性：

请求 [books.xml](https://www.w3school.com.cn/example/xmle/books.xml) 文件，并解析响应：

```html
xmlDoc=xmlhttp.responseXML;
txt="";
x=xmlDoc.getElementsByTagName("ARTIST");
for (i=0;i<x.length;i++)
  {
  txt=txt + x[i].childNodes[0].nodeValue + "<br />";
  }
document.getElementById("myDiv").innerHTML=txt;
```



##### XHR readyState

onreadystatechange 事件：

当请求被发送到服务器时，我们需要执行一些基于响应的任务。每当 readyState 改变时，就会触发 onreadystatechange 事件。readyState 属性存有 XMLHttpRequest 的状态信息。

下面是 XMLHttpRequest 对象的三个重要的属性：

| 属性               | 描述                                                         |
| ------------------ | ------------------------------------------------------------ |
| onreadystatechange | 存储函数（或函数名），每当 readyState 属性改变时，就会调用该函数。 |
| readyState         | 存有 XMLHttpRequest 的状态。从 0 到 4 发生变化。0: 请求未初始化                                  1: 服务器连接已建立                                                                                                                     2: 请求已接收                                                                                                                                3: 请求处理中                                                                                                                                4: 请求已完成，且响应已就绪 |
| status             | 200: "OK"                                                                                                                                      404: 未找到页面 |

在 onreadystatechange 事件中，我们规定当服务器响应已做好被处理的准备时所执行的任务。

当 readyState 等于 4 且状态为 200 时，表示响应已就绪：

```html
xmlhttp.onreadystatechange=function()
  {
  if (xmlhttp.readyState==4 && xmlhttp.status==200)
    {
    document.getElementById("myDiv").innerHTML=xmlhttp.responseText;
    }
  }
```


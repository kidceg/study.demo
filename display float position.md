# margin padding border 

![191935269513751](E:\Github+Desktop+for+win\gith..tion_317444273a93ac29_0003.0000_4d58bde1c4cef1d4\Githut\study.demo\191935269513751.gif)

![1](E:\Github+Desktop+for+win\gith..tion_317444273a93ac29_0003.0000_4d58bde1c4cef1d4\Githut\study.demo\1.gif)



![191935386296017](E:\Github+Desktop+for+win\gith..tion_317444273a93ac29_0003.0000_4d58bde1c4cef1d4\Githut\study.demo\191935386296017.jpg)



![191935495578126](E:\Github+Desktop+for+win\gith..tion_317444273a93ac29_0003.0000_4d58bde1c4cef1d4\Githut\study.demo\191935495578126.jpg)

![191936015368948](E:\Github+Desktop+for+win\gith..tion_317444273a93ac29_0003.0000_4d58bde1c4cef1d4\Githut\study.demo\191936015368948.jpg)



当上下、左右margin值分别一致, 可简写为:前一个40px代表上下margin值，后一个40px代表左右margin值。

```
margin: 40px 40px; 
```

当上下左右margin值均一致，可简写为:

```
margin: 40px;
```

![191936129093657](E:\Github+Desktop+for+win\gith..tion_317444273a93ac29_0003.0000_4d58bde1c4cef1d4\Githut\study.demo\191936129093657.jpg)

# display

　　display属性用于规定元素生成的框类型

　　初始值: inline

　　应用于: 所有元素

## 分类

### block

**块级元素特点：**

- **总是以一个块的形式表现出来，占领一整行。若干同级块元素会从上之下依次排列（使用float属性除外）。**
- **可以设置高度、宽度、各个方向外补丁（margin）以及各个方向的内补丁（padding）。**
- **不设置宽度时，宽度为父元素宽度，（是其容器的100%），除非我们给它设定了固定的宽度。**
- **块级元素中可以容纳其他块级元素或行内元素。**
- **常见的块级元素由<p><div><h1><li>等等。**
- **块级元素的display属性值默认为block。**

**【标签】**

```
<address>
<article>
<body>
<div>
<footer>
<form>
<h1>
<hr>
<html>
<nav>
<ol>
<p>
<section>
<ul>
```

**【不支持的样式】**

　　[1]vertical-align



### inline

**行内元素特点：**

- **它不会单独占据一整行，而是只占领自身的宽度和高度所在的空间。内容撑开宽度。若干同级行内元素会从左到右（即某个行内元素可以和其他行内元素共处一行），从上到下依次排列。**

- **行内元素不可以设置高度、宽度，其高度一般由其字体的大小来决定，其宽度由内容的长度控制。**

- **行内元素只能设置左右的margin值和左右的padding值，而不能设置上下的margin值和上下的padding值。因此我们可以通过设置左右的padding值来改变行内元素的宽度。**

- **常见的行内元素由<a><em><img>等等。**

- **行内元素一般不可以包含块级元素。**

- **行内元素的display属性值默认为inline。**

- **代码换行被解析成空格**

  【解决之一】：【先设定子元素字体，再设置父元素font-size:0px;////chrome中：-webkit-text-size-adjust:none】 fontsize为0，只要我们将ul中的字符的大小设置为0，那么空白符也就不会存在了，但是这是a的字体大小也会**继承**ul的字体大小，那么就不见了，该怎么办，只需要将a中再设置一个字体不为0的大小覆盖即可。 对于Chrome, 其默认有最小字体大小限制，考虑到兼容性，需要取消字体大小限制，这样写：.demo {font-size: 0;-webkit-text-size-adjust:none;}   这种方法在Safari不兼容；

  【解决方法二】：float:left

  【解决方法三】全兼容

  使用纯CSS还是找到了兼容的方法，就是在父元素中设置font-size:0,用来兼容chrome等浏览器，而使用letter-space:-N px来兼容safari:
```css
  .finally-solve {
    letter-spacing: -4px;/*根据不同字体字号或许需要做一定的调整*/
    word-spacing: -4px;
    font-size: 0;
  }
  .finally-solve li {
    font-size: 16px;
    letter-spacing: normal;
    word-spacing: normal;
    display:inline-block;
    *display: inline;
    zoom:1;
  }
```


【标签】**

```
<a>
<br>
<em>
<i>
<label>
<map>
<span>
<strong>
```

**【不支持的样式】**

　　[1]background-position

　　[2]clear

　　[3]clip

　　[4]height | max-height | min-height

　　[5]width | max-width | min-width

　　[6]overflow

　　[7]text-align

　　[8]text-indent

　　[9]text-overflow

【应用】

 **通过对一个行内元素设置display:　block;可以将行内元素设置为块级元素，进而设置它的宽高和上下左右的padding和margin。**

**display:inline的作用即可以将一个块级元素转换成行内元素，那么这个块级元素将不能再设置宽和高以及上下方向的margin和padding。**



### inline-block

 **它是结合了inline和block的特性于一身。既具有block元素可以设置width和height属性的特性，又保持了inline元素不换行的特性。**

**【特征】**

　　[1]不设置宽度时，内容撑开宽度

　　[2]非独占一行

　　[3]支持宽高

　　[4]代码换行被解析成空格【解决方法同上inline的】

**【标签】**

```
<img>
<input>
<audio>
<button>
<canvas>
<select>
<video>
```

**【不支持的样式】**

　　[1]clear

 【IE兼容】

　　IE7-浏览器不支持给块级元素设置inline-block样式，解决方法如下：首先将其变成行内元素，使用具有行内元素的特性，然后触发haslayout，使其具有块级元素的特性，如此就可以模拟出inline-block的效果

```
div{
    display:inline-block;
    *display: inline;
    zoom: 1;
```

### none

**【特征】**

　　隐藏元素并脱离文档流

**【标签】**

```
<base>
<link>
<meta>
<title>
<datalist><dialog><param>
<script>
<source>
<style>
```



 ### inherit

规定应该从父元素继承 display 属性的值

 



# float

float 属性定义元素在哪个方向浮动。以往这个属性总应用于图像，使文本围绕在图像周围，不过在 CSS 中，任何元素都可以浮动。浮动元素会生成一个块级框，而不论它本身是何种元素。假如在一行之上只有极少的空间可供浮动元素，那么这个元素会跳至下一行，这个过程会持续到某一行拥有足够的空间为止。



【特征】脱离文档流（HTML页面的标准文档流(默认布局)是：从上到下，从左到右，遇块(块级元素)换行。），进行左右浮动，紧贴着父元素(默认为body文本区域)的左右边框。

而此浮动元素在文档流空出的位置，由后续的(非浮动)元素填充上去：块级元素直接填充上去，若跟浮动元素的范围发生重叠，浮动元素覆盖块级元素。内联元素：有空隙就插入。

### 清除浮动的方法

让我们先说主流的方法：

clear: both/left/right
除了“none”以外的任何属性值都将导致元素相应位置不允许浮动。

overflow: hidden/auto
float导致了元素坍塌，如果你想让父元素包含所有的float属性元素，那么考虑在父元素上使用overlow:hidden/auto

clearfix
最好的方法是使用clearfix属性，下面的代码适用到IE6。

```
.clearfix:before,
.clearfix:after {
    content: " ";
    display: table;
}
.clearfix:after {
    clear: both;
}
/* For IE 6/7 only */
.clearfix {
    *zoom: 1;
}
```


如果你想适应IE8及其以上的，只要
```
.clearfix:after {
  content: "";
  display: table;
  clear: both;
}
```


你所要做的就是将clearfix类添加到包含floated的父元素上，你当然也可以使用overlow:hidden但是会导致很多布局上的其他问题。



# position

常用有relative、absolute、fixed

### absolute

生成绝对定位的元素，相对于 static 定位以外的第一个父元素进行定位。

元素的位置通过 "left", "top", "right" 以及 "bottom" 属性进行规定。

### fixed

生成绝对定位的元素，相对于浏览器窗口进行定位。

元素的位置通过 "left", "top", "right" 以及 "bottom" 属性进行规定。

### relative

生成相对定位的元素，相对于其正常位置进行定位。

因此，"left:20" 会向元素的 LEFT 位置添加 20 像素。

### static

默认值。没有定位，元素出现在正常的流中（忽略 top, bottom, left, right 或者 z-index 声明）。

### inherit

规定应该从父元素继承 position 属性的值。

# Mozilla建议的CSS书写顺序

/* Suggested order:
//显示属性

* display
* list-style
* position
* float
* clear
  //自身属性
* width
* height
* margin
* padding
* border
* background
  //文本属性
* color
* font
* text-decoration
* text-align
* vertical-align
* white-space
* other text
* content
  *
  */

移动端 的宽高

![241757572625462](E:\Github+Desktop+for+win\gith..tion_317444273a93ac29_0003.0000_4d58bde1c4cef1d4\Githut\study.demo\241757572625462.jpg)

![241806078874740](E:\Github+Desktop+for+win\gith..tion_317444273a93ac29_0003.0000_4d58bde1c4cef1d4\Githut\study.demo\241806078874740.jpg)

![241821417469973](E:\Github+Desktop+for+win\gith..tion_317444273a93ac29_0003.0000_4d58bde1c4cef1d4\Githut\study.demo\241821417469973.jpg)



# localStorage

首先在使用localStorage的时候，我们需要判断**浏览器是否支持localStorage这个属性**

localStorage本身的特点有关，localStorage只支持string类型的存储。

```javascript
if(！window.localStorage){
            alert("浏览器支持localstorage");
            return false;
        }else{
            //主逻辑业务
        }
```

### localStorage的写入，

*localStorage的写入**有三种方法

```javascript
if(！window.localStorage){
            alert("浏览器支持localstorage");
            return false;
        }else{
            var storage=window.localStorage;
            //写入a字段
            storage["a"]=1;
            //写入b字段
            storage.a=1;
            //写入c字段
            storage.setItem("c",3);
            console.log(typeof storage["a"]);
            console.log(typeof storage["b"]);
            console.log(typeof storage["c"]);
        }
```

![728493-20160626105220610-1095267293](E:\Github+Desktop+for+win\gith..tion_317444273a93ac29_0003.0000_4d58bde1c4cef1d4\Githut\study.demo\728493-20160626105220610-1095267293.png)

### localStorage的读取

```javascript
if(!window.localStorage){
            alert("浏览器支持localstorage");
        }else{
            var storage=window.localStorage;
            //写入a字段
            storage["a"]=1;
            //写入b字段
            storage.a=1;
            //写入c字段
            storage.setItem("c",3);
            console.log(typeof storage["a"]);
            console.log(typeof storage["b"]);
            console.log(typeof storage["c"]);
            //第一种方法读取
            var a=storage.a;
            console.log(a);
            //第二种方法读取
            var b=storage["b"];
            console.log(b);
            //第三种方法读取
            var c=storage.getItem("c");
            console.log(c);
        }
```

### localStorage的删、改这两个步骤

```javascript
if(!window.localStorage){
            alert("浏览器支持localstorage");
        }else{
            var storage=window.localStorage;
            //写入a字段
            storage["a"]=1;
            //写入b字段
            storage.b=1;
            //写入c字段
            storage.setItem("c",3);
            console.log(storage.a);
            // console.log(typeof storage["a"]);
            // console.log(typeof storage["b"]);
            // console.log(typeof storage["c"]);
            /*分割线*/
            storage.a=4;
            console.log(storage.a);
        }
```

这个在控制台上面我们就可以看到已经a键已经被更改为4了

**localStorage的删除**

1、将localStorage的所有内容清除

```javascript
var storage=window.localStorage;
            storage.a=1;
            storage.setItem("c",3);
            console.log(storage);
            storage.clear();
            console.log(storage);
```

2、 将localStorage中的某个键值对删除

```javascript
var storage=window.localStorage;
            storage.a=1;
            storage.setItem("c",3);
            console.log(storage);
            storage.removeItem("a");
            console.log(storage.a);
```

控制台查看结果

![728493-20160626115232188-571332017](E:\Github+Desktop+for+win\gith..tion_317444273a93ac29_0003.0000_4d58bde1c4cef1d4\Githut\study.demo\728493-20160626115232188-571332017.png)

### localStorage的键获取

```javascript
var storage=window.localStorage;
            storage.a=1;
            storage.setItem("c",3);
            for(var i=0;i<storage.length;i++){
                var key=storage.key(i);
                console.log(key);
            }
```

使用key()方法，向其中出入索引即可获取对应的键

一般我们会将JSON存入localStorage中，但是在localStorage会自动将localStorage转换成为字符串形式

这个时候我们可以使用JSON.stringify()这个方法，来将JSON转换成为JSON字符串

### JSON.stringify()

```javascript
if(!window.localStorage){
            alert("浏览器支持localstorage");
        }else{
            var storage=window.localStorage;
            var data={
                name:'xiecanyong',
                sex:'man',
                hobby:'program'
            };
            var d=JSON.stringify(data);
            storage.setItem("data",d);
            console.log(storage.data);
        }
```

读取之后要将JSON字符串转换成为JSON对象，使用JSON.parse()方法

### JSON.parse()

```javascript
var storage=window.localStorage;
            var data={
                name:'xiecanyong',
                sex:'man',
                hobby:'program'
            };
            var d=JSON.stringify(data);
            storage.setItem("data",d);
            //将JSON字符串转换成为JSON对象输出
            var json=storage.getItem("data");
            var jsonObj=JSON.parse(json);
            console.log(typeof jsonObj);
```

![728493-20160626124919578-638115637](E:\Github+Desktop+for+win\gith..tion_317444273a93ac29_0003.0000_4d58bde1c4cef1d4\Githut\study.demo\728493-20160626124919578-638115637.png)

打印出来是Object对象

另外还有一点要注意的是，其他类型读取出来也要进行转换

# sessionStorage 

需求方要求用户在一个列表页浏览时，点击一个列表进入详情页，返回要求记录用户刚刚浏览的位置，而不是重新刷新页面到了页面顶部。

sessionStorage - 针对一个 session 的数据存储（**关闭窗口，存储的数据清空**）

再理一下实现思路，①页面滚动，将滚动位置存到session中 → ②再次进到页面中，到session中取出上次保存的浏览位置 → ③滚动到对应位置

#### setItem存储value

　　用途：将value存储到key字段
　　用法：.setItem( key, value)
　　代码示例：

```javascript
 sessionStorage.setItem("key", "value"); 	localStorage.setItem("site", "js8.in");
```

#### 　　getItem获取value

　　用途：获取指定key本地存储的值
　　用法：.getItem(key)
　　代码示例：

```javascript
var value = sessionStorage.getItem("key"); 	
var site = localStorage.getItem("site");

//滚动时保存滚动位置
```

```javascript
$(window).scroll(function() {
if($(document).scrollTop() != 0) {
　　　　sessionStorage.setItem("offsetTop", $(window).scrollTop());//保存滚动位置
　　　　　　　} 
});
```

//onload时，取出并滚动到上次保存位置

```javascript
window.onload = function() {
　　var _offset = sessionStorage.getItem("offsetTop");

　　$(document).scrollTop(offsetTop);

};
```

 # 学习cookie----来自博客园转载

##什么是 Cookie

　　“cookie 是存储于访问者的计算机中的变量。每当同一台计算机通过浏览器请求某个页面时，就会发送这个 cookie。你可以使用 JavaScript 来创建和取回 cookie 的值。” - w3school
　　cookie 是访问过的网站创建的文件，用于存储浏览信息，例如个人资料信息。

　　从JavaScript的角度看，cookie 就是一些字符串信息。这些信息存放在客户端的计算机中，用于客户端计算机与服务器之间传递信息。

　　在JavaScript中可以通过 document.cookie 来读取或设置这些信息。由于 cookie 多用在客户端和服务端之间进行通信，所以除了JavaScript以外，服务端的语言（如PHP）也可以存取 cookie。

 

##Cookie 基础知识

- cookie 是有大小限制的，每个 cookie 所存放的数据不能超过4kb，如果 cookie 字符串的长度超过4kb，则该属性将返回空字符串。
- 由于 cookie 最终都是以文件形式存放在客户端计算机中，所以查看和修改 cookie 都是很方便的，这就是为什么常说 cookie 不能存放重要信息的原因。
- 每个 cookie 的格式都是这样的：<cookie名>=<值>；名称和值都必须是合法的标示符。
- cookie 是存在 有效期的。在默认情况下，一个 cookie 的生命周期就是在浏览器关闭的时候结束。如果想要 cookie 能在浏览器关掉之后还可以使用，就必须要为该 cookie 设置有效期，也就是 cookie 的失效日期。
- alert(typeof document.cookie)　　结果是 string，曾经我以为是array，还闹过笑话...囧
- cookie 有**域和路径**这个概念。域就是domain的概念，因为浏览器是个注意安全的环境，所以不同的域之间是不能互相访问 cookie 的(当然可以通过特殊设置的达到 cookie 跨域访问)。路径就是routing的概念，一个网页所创建的 cookie 只能被与这个网页在同一目录或子目录下得所有网页访问，而不能被其他目录下得网页访问（这句话有点绕，一会看个例子就好理解了）。
- 其实创建cookie的方式和定义变量的方式有些相似，都需要使用 cookie 名称和 cookie 值。同个网站可以创建多个 cookie ，而多个 cookie 可以存放在同一个cookie 文件中。



##Cookie常见问题

- cookie 存在两种类型：
  - 你浏览的当前网站本身设置的 cookie
  - 来自在网页上嵌入广告或图片等其他域来源的 第三方 cookie (网站可通过使用这些 cookie 跟踪你的使用信息)


- 刚刚基础知识里面有说到 cookie 生命周期的问题，其实 cookie 大致可分为两种状态：
  - 临时性质的cookie。当前使用的过程中网站会储存一些你的个人信息，当浏览器关闭后这些信息也会从计算机中删除
  - 设置失效时间的cookie。就算浏览器关闭了，这些信息业依然会在计算机中。如 登录名称和密码，这样无须在每次到特定站点时都进行登录。这种cookie 可在计算机中保留几天、几个月甚至几年
- cookie 有两种清除方式：
  - 通过浏览器工具清除 cookie (有第三方的工具，浏览器自身也有这种功能)
  - 通过设置 cookie 的有效期来清除 cookie
  - 注：删除 cookie 有时可能导致某些网页无法正常运行
- 浏览器可以通过设置来接受和拒绝访问 cookie。
- 出于功能和性能的原因考虑，建议尽量降低 cookie 的使用数量，并且要尽量使用小 cookie。
- 关于cookie编码的细节问题将会在cookie高级篇中单独介绍。
- 假如是本地磁盘中的页面，chrome的控制台是无法用JavaScript读写操作 cookie 的，解决办法...换一个浏览器^_^。



##Cookie基础用法

###一.简单的存取操作

　　在使用JavaScript存取 cookie 时，必须要使用Document对象的 cookie 属性；一行代码介绍如何创建和修改一个 cookie ：

```javascript
　　document.cookie  = 'username=Darren'
```

　　以上代码中'username'表示 cookie 名称，'Darren'表示这个名称对应的值。假设 cookie 名称并不存在，那么就是创建一个新的 cookie；如果存在就是修改了这个 cookie 名称对应的值。如果要多次创建 cookie ，重复使用这个方法即可。

 

###二.cookie的读取操作

　　要精确的对 cookie 进行读取其实很简单，就是对字符串进行操作。从w3school上copy这段代码来做分析：

```javascript
function getCookie(c_name){
　　　　if (document.cookie.length>0){　　//先查询cookie是否为空，为空就return ""
　　　　　　c_start=document.cookie.indexOf(c_name + "=")　　//通过String对象的indexOf()来检查这个cookie是否存在，不存在就为 -1　　
　　　　　　if (c_start!=-1){ 
　　　　　　　　c_start=c_start + c_name.length+1　　//最后这个+1其实就是表示"="号啦，这样就获取到了cookie值的开始位置
　　　　　　　　c_end=document.cookie.indexOf(";",c_start)　　//其实我刚看见indexOf()第二个参数的时候猛然有点晕，后来想起来表示指定的开始索引的位置...这句是为了得到值的结束位置。因为需要考虑是否是最后一项，所以通过";"号是否存在来判断
　　　　　　　　if (c_end==-1) c_end=document.cookie.length　　
　　　　　　　　return unescape(document.cookie.substring(c_start,c_end))　　//通过substring()得到了值。想了解unescape()得先知道escape()是做什么的，都是很重要的基础，想了解的可以搜索下，在文章结尾处也会进行讲解cookie编码细节
　　　　　　} 
　　　　}
　　　　return ""
　　}　　
```


　　当然想实现读取cookie的方法还有不少，比如数组，正则等，这里就不往细说了。

 

###三.设置cookie的有效期

　　文章中常常出现的 cookie 的生命周期也就是有效期和失效期，即 cookie 的存在时间。在默认的情况下，cookie 会在浏览器关闭的时候自动清除，但是我们可以通过expires来设置 cookie 的有效期。语法如下：
```javascript
　　document.cookie = "name=value;expires=date"
```

　　上面代码中的date值为GMT(格林威治时间)格式的日期型字符串，生成方式如下：

```javascript
　　var _date = new Date();
　　_date.setDate(_date.getDate()+30);
　　_date.toGMTString();
```

　　上面三行代码分解为几步来看：

- 通过new生成一个Date的实例，得到当前的时间；
- getDate()方法得到当前本地月份中的某一天，接着加上30就是我希望这个cookie能过在本地保存30天；
- 接着通过setDate()方法来设置时间；
- 最后 用toGMTString()方法把Date对象转换为字符串，并返回结果

　　通过下面这个完整的函数来说明在创建 cookie 的过程中我们需要注意的地方 - 从w3school复制下来的。创建一个在 cookie 中存储信息的函数：

```javascript
 　function setCookie(c_name, value, expiredays){
 　　　　var exdate=new Date();
 　　　　exdate.setDate(exdate.getDate() + expiredays);
 　　　　document.cookie=c_name+ "=" + escape(value) + ((expiredays==null) ? "" : ";expires="+exdate.toGMTString());
 　　}
 　　使用方法：setCookie('username','Darren',30)  
```


　　现在我们这个函数是按照天数来设置cookie的有效时间，如果想以其他单位（如：小时）来设置，那么改变第三行代码即可：

```javascript
　　exdate.setHours(exdate.getHours() + expiredays);
```

　　这样设置以后的cookie有效期就是按照小时为单位的。

　　常见问题中有提到清除 cookie 的两种方法，现在要说的是使 cookie 失效，通过把有效期的时间设置为一个已过期的时间。既然已经有了设置有效期的方法，那么设置失效期的方法就请感兴趣的朋友自己动手了^_^。下面继续比较深的cookie话题。

 

##Cookie 高级篇

###一.cookie 路径概念

　　在基础知识中有提到 cookie 有域和路径的概念，现在来介绍路径在 cookie 中的作用。

　　cookie 一般都是由于用户访问页面而被创建的，可是并不是只有在创建 cookie 的页面才可以访问这个 cookie。

　　默认情况下，只有与创建 cookie 的页面在同一个目录或子目录下的网页才可以访问，这个是因为安全方面的考虑，造成不是所有页面都可以随意访问其他页面创建的 cookie。举个例子：

　　在 "http://www.cnblogs.com/Darren_code/" 这个页面创建一个cookie，那么在"/Darren_code/"这个路径下的页面如： "http://www.cnblogs.com/Darren_code/archive/2011/11/07/Cookie.html"这个页面默认就能取到cookie信息。

　　可在默认情况下， "http://www.cnblogs.com"或者 "http://www.cnblogs.com/xxxx/" 就不可以访问这个 cookie

　　那么如何让这个 cookie 能被其他目录或者父级的目录访问类，通过设置 cookie 的路径就可以实现。例子如下：

```javascript
　　document.cookie = "name=value;path=path"
　　document.cookie = "name=value;expires=date;path=path"
```

 　　红色字体path就是 cookie 的路径，最常用的例子就是让 cookie 在跟目录下,这样不管是哪个子页面创建的 cookie，所有的页面都可以访问到了:

```javascript
　　document.cookie = "name=Darren;path=/"
```

　　 

###二.cookie 域概念

　　路径能解决在同一个域下访问 cookie 的问题，咱们接着说 cookie 实现**同域**之间访问的问题。语法如下：

```javascript
　　document.cookie = "name=value;path=path;domain=domain"
```

　　红色的domain就是设置的 cookie 域的值。

　　例如 "www.qq.com" 与 "sports.qq.com" 公用一个关联的域名"qq.com"，我们如果想让 "sports.qq.com" 下的cookie被 "www.qq.com" 访问，我们就需要用到 cookie 的domain属性，并且需要把path属性设置为 "/"。例：

```javascript
　　document.cookie = "username=Darren;path=/;domain=qq.com"
```

　　注：一定的是同域之间的访问，不能把domain的值设置成非主域的域名。

 

###三.cookie 安全性

　　通常 cookie 信息都是使用HTTP连接传递数据，这种传递方式很容易被查看，所以 cookie 存储的信息容易被窃取。假如 cookie 中所传递的内容比较重要，那么就要求使用加密的数据传输。

　　所以 cookie 的这个属性的名称是“secure”，默认的值为空。如果一个 cookie 的属性为secure，那么它与服务器之间就通过HTTPS或者其它安全协议传递数据。语法如下：

```javascript
　　document.cookie = "username=Darren;secure"
```

　　把cookie设置为secure，只保证 cookie 与服务器之间的数据传输过程加密，而保存在本地的 cookie文件并不加密。如果想让本地cookie也加密，得自己加密数据。

　　注：就算设置了secure 属性也并不代表他人不能看到你机器本地保存的 cookie 信息，所以说到底，别把重要信息放cookie就对了，囧...

　　 

###四.cookie 编码细节

　　原本来想在常见问题那段介绍cookie编码的知识，因为如果对这个不了解的话编码问题确实是一个坑，所以还是详细说说。

　　在输入cookie信息时不能包含空格，分号，逗号等特殊符号，而在一般情况下，cookie 信息的存储都是采用未编码的方式。所以，在设置 cookie 信息以前要先使用escape()函数将 cookie 值信息进行编码，在获取到 cookie 值得时候再使用unescape()函数把值进行转换回来。如设置cookie时：

```javascript
　　document.cookie = name + "="+ escape (value)
```

　　再看看基础用法时提到过的getCookie()内的一句：

```
　　return unescape(document.cookie.substring(c_start,c_end))
```

　　这样就不用担心因为在cookie值中出现了特殊符号而导致 cookie 信息出错了。

##运用JS设置cookie、读取cookie、删除cookie

###JS设置cookie:

假设在A页面中要保存变量username的值("jack")到cookie中,key值为name，则相应的JS代码为： 
```javascript
document.cookie="name="+username;  
```
###JS读取cookie:

假设cookie中存储的内容为：name=jack;password=123

则在B页面中获取变量username的值的JS代码如下：
```javascript
var username=document.cookie.split(";")[0].split("=")[1];  
```
###JS操作cookies方法!

###写cookies
```javascript
function setCookie(name,value) 
{ 
    var Days = 30; 
    var exp = new Date(); 
    exp.setTime(exp.getTime() + Days*24*60*60*1000); 
    document.cookie = name + "="+ escape (value) + ";expires=" + exp.toGMTString(); 
} 
```
###读取cookies
```javascript
function getCookie(name) 
{ 
   var arr,reg=new RegExp("(^| )"+name+"=([^;]*)(;|$)");

    if(arr=document.cookie.match(reg))

       return unescape(arr[2]); 
   else 
     return null; 
} 
```
###删除cookies
```javascript
function delCookie(name) 
{ 
​    var exp = new Date(); 
​    exp.setTime(exp.getTime() - 1); 
​    var cval=getCookie(name); 
​    if(cval!=null) 
​        document.cookie= name + "="+cval+";expires="+exp.toGMTString(); 
} 
```
//使用示例 
```javascript
setCookie("name","hayden"); 
alert(getCookie("name")); 
```
//如果需要设定自定义过期时间 
//那么把上面的setCookie　函数换成下面两个函数就ok; 


###程序代码 
```javascript
function setCookie(name,value,time)
{ 
    var strsec = getsec(time); 
    var exp = new Date(); 
    exp.setTime(exp.getTime() + strsec*1); 
    document.cookie = name + "="+ escape (value) + ";expires=" + exp.toGMTString(); 
} 
function getsec(str)
{ 
   alert(str); 
   var str1=str.substring(1,str.length)*1; 
   var str2=str.substring(0,1); 
   if (str2=="s")
   { 
        return str1*1000; 
   }
   else if (str2=="h")
   { 
       return str1*60*60*1000; 
   }
   else if (str2=="d")
   { 
       return str1*24*60*60*1000; 
   } 
} 
```
//这是有设定过期时间的使用示例： 
//s20是代表20秒 
//h是指小时，如12小时则是：h12 
//d是天数，30天则：d30 
```javascript
setCookie("name","hayden","s20");
```

### 本地文件创建一个cookie不生效，会是什么原因导致？
出于安全考虑，chrome本地环境cookie是禁止的，可以给他个服务器环境，或者用firebox。



# jquery 使用方法



##### 一、选择网页元素

jQuery的基本设计和主要用法，就是"选择某个网页元素，然后对其进行某种操作"。这是它区别于其他函数库的根本特点。

　　　　使用jQuery的第一步，往往就是将一个选择表达式，放进构造函数jQuery()(简写为$)，然后得到被选中的元素。

选择表达式可以是CSS选择器：

 

```JavaScript
1 $(document)//选择整个文档对象
2 $('#myId')//选择ID为myId的网页元素  
3 $('div.myClass')//选择class为myClass的div元素    
4 $('input[name=first]')//选择name属性等于first的input元素
```

也可以是jQuery特有的表达式：

```JavaScript
1 $('a:first')//选择网页中第一个a元素  
2 $('tr:odd')//选择表格的奇数行  
3 $('#myForm :input')//选择表单中的input元素  
4 $('div:visible') //选择可见的div元素  
5 $('div:gt(2)')//选择所有的div元素，除了前三个  
6 $('div:animated')//选择当前处于动画状态的div元素  
```
##### 二、改变结果集

如果选中多个元素，jQuery提供过滤器，可以缩小结果集：

```JavaScript
1 $('div').has('p'); //选择包含p元素的div元素  
2 $('div').not('.myClass'); //选择class不等于myClass的div元素  
3 $('div').filter('.myClass'); //选择class等于myClass的div元素  
4 $('div').first(); //选择第1个div元素  
5 $('div').eq(5); //选择第6个div元素  
```

有一些时候，我们需要从结果集出发，移动到附近的相关元素，jQuery也提供了在DOM树上的移动方法：

```JavaScript
1 $('div').next('p'); //选择div元素后面的第一个p元素  
2 $('div').parent(); //选择div元素的父元素  
3 $('div').closest('form'); //选择离div最近的那个form父元素  
4 $('div').children(); //选择div的所有子元素  
5 $('div').siblings(); //选择div的同级元素  
```

##### 三、链式操作

选中网页元素以后，就可以对它进行某种操作。

jQuery允许将所有操作连接在一起，以链条的形式写出来，比如：

```JavaScript
1 $('div').find('h3').eq(2).html('Hello');  
```

我们可以这样拆封开来，就是下面这样：

```JavaScript
1 $('div')//找到div元素  
2 .find('h3')//选择其中的h3元素  
3 .eq(2)//选择第3个h3元素  
4 .html('Hello'); //将它的内容改为Hello  
```

 

这是jQuery最令人称道、最方便的特点。它的原理在于每一步的jQuery操作，返回的都是一个jQuery对象，所以不同操作可以连在一起。

jQuery还提供了.end()方法，使得结果集可以后退一步：

```JavaScript
1 $('div')  
2 .find('h3')  
3 .eq(2)  
4 .html('Hello')  
5 .end()//退回到选中所有的h3元素的那一步  
6 .eq(0)//选中第一个h3元素  
7 .html('World'); //将它的内容改为World  
```
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

 




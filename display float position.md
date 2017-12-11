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

- **块级元素的display属性值默认为inline。**

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



# position


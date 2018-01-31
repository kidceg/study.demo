# CSS命名规则

CSS命名规则

　　头：header

　　内容：content/containe

　　尾：footer

　　导航：nav

　　侧栏：sidebar

　　栏目：column

　　页面外围控制整体布局宽度：wrapper

　　左右中：left right center

　　登录条：loginbar

　　标志：logo

　　广告：banner

　　页面主体：main

　　热点：hot

　　新闻：news

　　下载：download

　　子导航：subnav

　　菜单：menu

　　子菜单：submenu

　　搜索：search

　　友情链接：friendlink

　　页脚：footer

　　版权：copyright

　　滚动：scroll

　　内容：content

　　标签页：tab

　　文章列表：list

　　提示信息：msg

　　小技巧：tips

　　栏目标题：title

　　加入：joinus

　　指南：guild

　　服务：service

　　注册：regsiter

　　状态：status

　　投票：vote

　　合作伙伴：partner

XHTML文件中id的命名

(1)页面结构

　　容器: container

　　页头：header

　　内容：content/container

　　页面主体：main

　　页尾：footer

　　导航：nav

　　侧栏：sidebar

　　栏目：column

　　页面外围控制整体布局宽度：wrapper

　　左右中：left right center

(2)导航

　　导航：nav

　　主导航：mainbav

　　子导航：subnav

　　顶导航：topnav

　　边导航：sidebar

　　左导航：leftsidebar

　　右导航：rightsidebar

　　菜单：menu

　　子菜单：submenu

　　标题: title

　　摘要: summary

(3)功能

　　标志：logo

　　广告：banner

　　登陆：login

　　登录条：loginbar

　　注册：regsiter

　　搜索：search

　　功能区：shop

　　标题：title

　　加入：joinus

　　状态：status

　　按钮：btn

　　滚动：scroll

　　标签页：tab

　　文章列表：list

　　提示信息：msg

　　当前的: current

　　小技巧：tips

　　图标: icon

　　注释：note

　　指南：guild

　　服务：service

　　热点：hot

　　新闻：news

　　下载：download

　　投票：vote

　　合作伙伴：partner

　　友情链接：link

　　版权：copyright

 



# calc基本用法

**calc基本语法：**
```
 .class {width: calc(expression);}
```
 它可以支持加，减，乘，除; 在我们做手机端的时候非常有用的一个知识点;
 优点如下：
 \1. 支持使用 "+","-","*" 和 "/" 四则运算。
 \2. 可以混合使用百分比(%),px,em,rem等作为单位可进行计算。
 浏览器的兼容性有如下：
 IE9+，FF4.0+，Chrome19+，Safari6+
 如下测试代码：
```
<div class="calc">我是测试calc</div>
```
```
.calc{
    margin-left:50px;
    padding-left:2rem;
    width:calc(100%-50px-2rem);
    height:10rem;
}
```
# 移动开发基本知识点

###一. 使用rem作为单位**

```
html { font-size: 100px; }
@media(min-width: 320px) { html { font-size: 100px; } }
@media(min-width: 360px) { html { font-size: 112.5px; } }
@media(min-width: 400px) { html { font-size: 125px; } }
@media(min-width: 640px) { html { font-size: 200px; } }
```

给手机设置100px的字体大小; 对于320px的手机匹配是100px，
其他手机都是等比例匹配; 因此设计稿上是多少像素的话，那么转换为rem的时候，rem = 设计稿的像素/100 即可;

###**二.  禁用a,button,input,optgroup,select,textarea 等标签背景变暗**

在移动端使用a标签做按钮的时候或者文字连接的时候，点击按钮会出现一个 "暗色的"背景，比如如下代码：
```
  <a href="">button1</a>
  <input type="button" value="提交"/>
```
在移动端点击后 会出现"暗色"的背景，这时候我们需要在css加入如下代码即可：

```
a,button,input,optgroup,select,textarea{
    -webkit-tap-highlight-color: rgba(0,0,0,0);
}
```
###**三. meta基础知识点：**

   1.页面窗口自动调整到设备宽度，并禁止用户及缩放页面。

```
<meta name="viewport" content="width=device-width, initial-scale=1.0, minimum-scale=1.0,maximum-scale=1.0, user-scalable=0" />
```

 属性基本含义：
  content="width=device-width：
  控制 viewport 的大小,device-width 为设备的宽度
  initial-scale - 初始的缩放比例
  minimum-scale - 允许用户缩放到的最小比例
  maximum-scale - 允许用户缩放到的最大比例
  user-scalable - 用户是否可以手动缩放

2.忽略将页面中的数字识别为电话号码
```
  <meta name="format-detection" content="telephone=no" />
```
 \3. 忽略Android平台中对邮箱地址的识别
  ``` <meta name="format-detection" content="email=no" />```

 \4. 当网站添加到主屏幕快速启动方式，可隐藏地址栏，仅针对ios的safari
``` <meta name="apple-mobile-web-app-capable" content="yes" />```

 \5. 将网站添加到主屏幕快速启动方式，仅针对ios的safari顶端状态条的样式
``` <meta name="apple-mobile-web-app-status-bar-style" content="black" />```

``` <!-- 可选default、black、black-translucent -->```
 \6. 需要在网站的根目录下存放favicon图标，防止404请求(使用fiddler可以监听到)，在页面上需加link如下：
``` <link rel="shortcut icon" href="/favicon.ico">```

因此页面上通用的模板如下：

```
<!DOCTYPE html>
 <html>
    <head>
        <meta charset="utf-8">
        <meta content="width=device-width,initial-scale=1.0,maximum-scale=1.0,user-scalable=no" name="viewport">
        <meta content="yes" name="apple-mobile-web-app-capable">
        <meta content="black" name="apple-mobile-web-app-status-bar-style">
        <meta content="telephone=no" name="format-detection">
        <meta content="email=no" name="format-detection">
        <title>标题</title>
        <link rel="shortcut icon" href="/favicon.ico">
    </head>
    <body>
        这里开始内容
    </body>
</html>
```
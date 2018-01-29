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
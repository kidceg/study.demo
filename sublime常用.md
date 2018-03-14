# 修改Sublime Text编辑器滚动条滑块颜色的方法

但Sublime Text也有些问题是我不喜欢的，比如，它的窗口滚动条滑块的颜色和背景太相似，以至于我很难找到滑块在哪里(我使用的是Sublime Text 3缺省的暗黑皮肤)。如图：

![XUSOu](http://www.vaikan.com/wordpress/wp-content/uploads/2016/07/XUSOu.png)

在晚上，或在你调暗电脑屏幕后，几乎看不到滚动条滑块在哪里。

Sublime Text编辑器有很强大的自定义功能，可以换肤，可以安装插件。下面，我将要讲一讲如何修改Sublime Text的滚动条滑块的颜色。

我使用的是Sublime Text 3。要修改Sublime Text的颜色，我们会首先想到修改主题皮肤的属性。我们可以在`Preferences.sublime-settings`里写一段代码覆盖掉原有主题的某些颜色属性。但问题是，Sublime Text的滑块颜色并不是只通过修改颜色就可以解决的，它的滑块实际上是用图片表现的，也就是说，你不仅要修改颜色，还要换图片。

所以，解决方法就是创建两个新的滚动条滑块图片(一个横向的，一个竖向的)，图片颜色要明亮些，然后，按照下面的步骤一步步设置。

## 修改Sublime Text滚动条颜色的步骤：

1、找到你的Sublime Text的“User”目录(Packages/User)。这个“Packages”目录你可以通过Sublime Text上的菜单“Preferences>Browse Packages”打开，就可以看到“User”目录。（在Linux系统里，这个目录通常位于“/home/username/.config/sublime-text-3/Packages/User”目录。）

2、在“User”目录下，创建一个叫“Theme – Default”的目录。我们将在这个目录里创建一个配置文件，来覆盖掉缺省主题皮肤的某些属性。

3、在“Theme – Default”目录下创建一个叫做“Default.sublime-theme”的文件，在文件里添加如下内容：

```
[
    // More visible scrollbar
    {
        "class": "puck_control",
        "layer0.texture": "User/Theme - Default/vertical_white_scrollbar.png",
        // Adjust RGB color. Optional: comment the following line (or set 255,255,255) to not modify image color
        "layer0.tint": [200, 170, 250]
    },
    {
        "class": "puck_control",
        "attributes": ["horizontal"],
        "layer0.texture": "User/Theme - Default/horizontal_white_scrollbar.png"
    }
]
```

4、在“Theme – Default”目录里，放入我们创建的两个新的、颜色更明亮的滑块图片，并命名如下：
*vertical_white_scrollbar.png (![p0ol7](http://www.vaikan.com/wordpress/wp-content/uploads/2016/07/p0ol7.png))*和*horizontal_white_scrollbar.png (![cbWTz](http://www.vaikan.com/wordpress/wp-content/uploads/2016/07/cbWTz.png)).*。（右键“图片另存为”可下载这两个图片）。

5、重启Sublime Text。

6、你还可以修改配置里的RGB颜色值来获得不同的润色，这种修改不需要重启Sublime Text。

修改完的效果如下图：



![ZF93E](http://www.vaikan.com/wordpress/wp-content/uploads/2016/07/ZF93E.png)





当主题更改后发现不完全的时候如何设置

在uer里面可设置theme,把theme后面对应的主题名称改成相对应的，就可以完整显示主题了









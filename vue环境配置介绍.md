1.安装node.js(http://www.runoob.com/nodejs/nodejs-install-setup.html)

2.基于node.js,利用淘宝npm镜像安装相关依赖

 在cmd里直接输入：npm install -g cnpm --registry=[https://registry.npm.taobao.org](https://registry.npm.taobao.org/)，回车，等待安装...

3.安装全局vue-cli脚手架,用于帮助搭建所需的模板框架

在cmd里 1)输入：cnpm install -g vue-cli，回车，等待安装...

​            2).输入：vue，回车，若出现vue信息说明表示成功

4.创建项目

在cmd里输入：vue init webpack vue_test(项目文件夹名)，回车，等待一小会儿，依次出现‘git’下的项，可按下图操作

![img](https://images2015.cnblogs.com/blog/1000531/201611/1000531-20161104114221752-1894187307.png)

5.安装依赖

在cmd里  1).输入：cd vue_test（项目名），回车，进入到具体项目文件夹

​             2).输入：cnpm install，回车，等待一小会儿

回到项目文件夹，会发现项目结构里，多了一个node_modules文件夹（该文件里的内容就是之前安装的依赖）

基于脚手架创建的默认项目结构如下图所示：

![img](https://images2015.cnblogs.com/blog/1000531/201611/1000531-20161104120244799-2006728410.png)

6.测试环境是否搭建成功

方法1：在cmd里输入：npm run dev

方法2：在浏览里输入：localhost:8080(默认端口为8080)

运行起来后的效果如下图所示：

![img](https://images2015.cnblogs.com/blog/1000531/201611/1000531-20161104121102221-395461091.png)

参照原文：http://blog.csdn.net/luckylqh/article/details/52863026
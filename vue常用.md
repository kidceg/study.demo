## Vue动画支持（transition）

以DIV从右到做的飞入动画为例。
在需要加动画的组建上设置属性：transition="动画名称"

```
<template>
  <div v-show="showFlag" transition="move" class="food">
  </div>
</template>
```

这里给要添加动画的组建设置了transition属性，并且值等于move，也就是去个名字

然后在style样式中分别写两个样式：

```
<style lang="less" rel="stylesheet/less">
  .food{
    // 其他样式
    ... ...
    &.move-transition{
      transition: all .2s linear;
      transform: translate3d(0,0,0);
    }
    &.move-enter,&.move-leave{
      transform: translate3d(100%,0,0);
    }
  }
</style>
```

样式以“动画名称-transition”为名，表示动画开始的设置，以“enter”“leave”结尾的表示动画结束的设置。

这样就完成了一个简单的Vue动画。

## 父组建调用子组件方法（v-ref）

parent组件中有child组件，并且在子组件上设置v-ref属性：

```
<template>
   // child组建
   <child v-ref:child></child>
</template>
<script type="text/ecmascript-6">
    export default{
        methods: {
            methodA() {
                // 调用子组件方法
                this.$refs.child.show();
            }
        }
    };
</script>
<style lang="less" rel="stylesheet/less">
</style>
```

注意：v-ref后面的值是以“:”连接的而不是“=”号。“this.$refs.child”就是获取到子组件。

child子组件内容

```
<template>
   <div>我是child组建</div>
</template>
<script type="text/ecmascript-6">
    export default{
        methods: {
            show() {
                //方法内容
            }
        }
    };
</script>
<style lang="less" rel="stylesheet/less">
</style>
```

## 子组建通知父组件（事件派发$dispatch）

在子组件方法中

```
this.$dispatch('content.toggle', type);
```

“ratingtype.select”是自定义事件名，在父组件中可以监听该事件，在父组件中定义events属性处理事件

```
events: {
      'ratingtype.select'(type) {
        this.selectType = type;
      },
      'content.toggle'(onlyContent) {
        this.onlyContent = onlyContent;
      }
}
```

## DOM绑定（v-el）

通过给div设置“v-el:xxx”就如同给div设置一个id属性，然后可以通过这个id获取DIV元素。

```
<div class="food" v-el:food>
```

然后在使用$els即可访问该元素

```
let food = this.$els.food;
```

food得到的就是一个DOM对象

## 阻止元素点击穿透和冒泡

```
<div @click.stop.prevent="test">test</div>
```

## 生命周期不重新加载（keep-alive）

在切换路由的时候不希望每次切换都重新被渲染一次，可以在路由出口上添加keep-alive属性即可

```
<router-view :user="user" keep-alive></router-view>
```

## 项目编译打包注意

使用vue-cli创建的项目使用npm run build命令进行打包编译成静态文件。但是可能遇到如下异常：

```
- building for production...shell.js: internal error
Error: ENOENT: no such file or directory, stat 'D:\xxxxxapp\static\*'
... ...
```

此时，可以尝试更新shelljs包的版本，如项目中shelljs当前版本是0.6.0，那么可以更新至0.7.4（npm update shelljs@0.7.4）后再次进行build命令

#Vue.js常用指令总结		

有时候指令太多会造成记错、记混的问题，所以本文在记忆的时候会采用穿插记忆的方式，交叉比对，不易出错。

本文主要讲了一下六个指令：

v-if//v-show//v-else//v-for//v-bind//v-on

\1. v-if 条件渲染指令，根据其后表达式的bool值进行判断是否渲染该元素；

eg:  

　　HTML: 
```
<div id="example01">
    <p v-if="male">Male</p>
    <p v-if="female">Female</p>
    <p v-if="age>25">Age:{{age}}</p>
    <p v-if="name.indexOf('lin')>0">Name:{{name}}</p>
</div>
```

　　JS:
```
var vm= new Vue({
        el:"#example01",
        data:{
            male:true,
            female: false,
            age:29,
            name:'colin'
        }
    })
```
页面渲染效果：

![img](https://images2015.cnblogs.com/blog/862173/201608/862173-20160814162621609-999115737.png)

所以，v-if指令只渲染他身后表达式为true的元素；在这里引入v-show指令，因为二者的区别是v-show指令会渲染他身后表达式为false的元素，这样的元素上会添加css代码：style="display:none"; 将上面v-if的实例代码改为v-show，页面渲染效果为：

![img](https://images2015.cnblogs.com/blog/862173/201608/862173-20160814163007687-760368450.png)

 

2, v-show 与v-if类似，只是会渲染其身后表达式为false的元素，而且会给这样的元素添加css代码：style="display:none";

3, v-else 必须跟在v-if/v-show指令之后，不然不起作用；

如果v-if/v-show指令的表达式为true，则else元素不显示；如果v-if/v-show指令的表达式为false，则else元素显示在页面上；

eg: 
```
<div id="app">
<h1 v-if="age >= 25">Age: {{ age }}</h1>
<h1 v-else>Name: {{ name }}</h1>
<hr>
<h1 v-show="name.indexOf('cool') = 0">Name: {{ name }}</h1>
<h1 v-else>Sex: {{ sex }}</h1>
</div>


<script>
    var vm = new Vue({
        el: '#app',
        data: {
            age: 21,
            name: 'keepcool',
            sex: 'Male'
        }
    })
</script>
```

4, v-for  类似JS的遍历，用法为 v-for="item in items", items是数组，item为数组中的数组元素。

eg:
```
CSS:
<style>
table,th,tr,td{
            border:1px solid #ffcccc;
            border-collapse: collapse;
        }
</style>
HTML:
<div id="example03">
    <table>
        <thead>
        <tr>
            <th>Name</th>
            <th>Age</th>
            <th>Sex</th>
        </tr>
        </thead>
        <tbody>
        <tr v-for="person in people">
            <td>{{ person.name  }}</td>
            <td>{{ person.age  }}</td>
            <td>{{ person.sex  }}</td>
        </tr>
        </tbody>
    </table>
</div>
JS:
<script>
    var vm = new Vue({
        el: '#example03',
        data: {
            people: [{
                name: 'Jack',
                age: 30,
                sex: 'Male'
            }, {
                name: 'Bill',
                age: 26,
                sex: 'Male'
            }, {
                name: 'Tracy',
                age: 22,
                sex: 'Female'
            }, {
                name: 'Chris',
                age: 36,
                sex: 'Male'
            }]
        }
    })
</script>
```

页面效果：

![img](https://images2015.cnblogs.com/blog/862173/201608/862173-20160814164529406-1638623608.png)

 

5, v-bind  这个指令用于响应地更新 HTML 特性，比如绑定某个class元素或元素的style样式。

eg,分页功能中当前页数高亮的效果，可以使用bind指令。

```
<ul class="pagination">
                <li v-for="n in pageCount">
                    <a href="javascripit:void(0)" v-bind:class="activeNumber === n + 1 ? 'active' : ''">{{ n + 1 }}</a>
                </li>
            </ul>
```

6, v-on  用于监听指定元素的DOM事件，比如点击事件。

eg:

```
<div id="example04">
        <input type="text" v-model="message">
        <button v-on:click="greet">Greet</button>
        <!-- v-on指令可以缩写为@符号-->
     <button @click="greet">Greet Again</button>
    </div>
<script>
    var exampleData04={
        message:"Nice meeting U"
    };
    var vm2=new Vue({
        el:"#example04",
        data:exampleData04,
        methods:{
            greet:function(){
                alert(this.message);
            }
         
        }
    })
</script>
```

# Vue实例常用属性

（1）数据

data:Vue 实例的数据对象

components：Vue实例配置局部注册组件

（2）类方法
computed:计算属性

watch：侦听属性

filters：过滤器

methods:Vue实例方法

render：渲染函数，创建虚拟DOM

（3）生命周期
created：在实例创建完成后被立即调用，完成初始化操作
mounted：el挂载到Vue实例上了，开始业务逻辑操作
beforeDestroy：实例销毁之前调用

 2、Vue组件

props:用于接收来自父组件的数据
template：组件模板

# 手机端看——草料二维码

https://cli.im/  草料二维码生成器

本地的http://localhost:8080怎么在手机上看呢

mac打开cmd输入ifconfig运行

Windows打开cmd输入ipconfig运行

查找到有一行显示：本地链接地址IPv6地址：10.0.0.4

把这个10.0.0.4替换到localhost，把原来的http://localhost:8080/#/goods改变成http://10.0.0.4:8080/#/goods

然后放到二维码生成器那里就可以用手机扫了看了

# sublime安装stylus插件

如果你使用sublime，你可以ctrl+shift+p调出控制台然后输入install package然后输入stylus然后回车安装，安装成功后在package settings你会看到如蓝色背景条所示
![img](https://segmentfault.com/img/bVvLAn)
展开蓝色背景条，在setting-user里面进行配置即可

```
{
    "envPATH": "",  //环境的路径 
    "binDir": "",   //项目路径
    "compileOnSave": true,  //是否编辑保存
    "compileDir": true,   //编译到指定目录
    "compress": true,  //是否压缩
    "compilePaths": {"": ""}  //输出路径
}
```

设置完成之后建立.styl文件，然后编辑保存，你就会在输出路径里面看到编译好的css文件了

# css sticky footers

https://www.w3cplus.com/css3/css-secrets/sticky-footers.html

# 最新的vue没有dev-server.js文件，如何进行后台数据模拟？ 

最新的vue-webpack-template 中已经去掉了dev-server.js 但是要进行模拟后台数据的，如何模拟本地数据操作？

解决方法： 
dev-server.js 改用webpack-dev-conf.js代替。 
所以在模拟后台数据的时候直接在webpack-dev-conf.js文件中修改：

```
const axios = require('axios')
const express = require('express')
const app = express()
const apiRoutes = express.Router()
app.use('/api', apiRoutes)12345
```

找到devServer配置项：

```
before(app) {
  app.get('/api/someApi', (req, res) => {
    res.json({
      // 这里是你的json内容
    })
  })
}1234567
```

这样就可以实现后台数据模拟，注意上面的依赖开发工具是否下载。





参照了别人写的记录一下

最新的vue里dev-server.js被替换成了webpack-dev-conf.js

在模拟后台数据的时候直接在webpack-dev-conf.js文件中修改

第一步，在const portfinder = require(‘portfinder’)后添加

```
//第一步
const express = require('express')
const app = express()//请求server
var appData = require('../data.json')//加载本地数据文件
var seller = appData.seller//获取对应的本地数据
var goods = appData.goods
var ratings = appData.ratings
var apiRoutes = express.Router()
app.use('/api', apiRoutes)//通过路由请求数据
```

第二步：找到devServer,在里面加上before（）方法

```
devServer: {
    clientLogLevel: 'warning',
    historyApiFallback: true,
    hot: true,
    compress: true,
    host: HOST || config.dev.host,
    port: PORT || config.dev.port,
    open: config.dev.autoOpenBrowser,
    overlay: config.dev.errorOverlay
      ? { warnings: false, errors: true }
      : false,
    publicPath: config.dev.assetsPublicPath,
    proxy: config.dev.proxyTable,
    quiet: true, // necessary for FriendlyErrorsPlugin
    watchOptions: {
      poll: config.dev.poll,
    },
    //第二步找到devServer,在里面添加
before(app) {
  app.get('/api/seller', (req, res) => {
    res.json({
      errno: 0,
      data: seller
    })//接口返回json数据，上面配置的数据seller就赋值给data请求后调用
  }),
  app.get('/api/goods', (req, res) => {
    res.json({
      errno: 0,
      data: goods
    })
  }),
  app.get('/api/ratings', (req, res) => {
    res.json({
      errno: 0,
      data: ratings
    })
  })
}
  }
```

提供一个data.json数据

```
{
  "seller": {
    "name": "粥品香坊（回龙观）",
    "description": "蜂鸟专送",
    "deliveryTime": 38,
    "score": 4.2,
    "serviceScore": 4.1,
    "foodScore": 4.3,
    "rankRate": 69.2,
    "minPrice": 20,
    "deliveryPrice": 4,
    "ratingCount": 24,
    "sellCount": 90,
    "bulletin": "粥品香坊其烹饪粥料的秘方源于中国千年古法，在融和现代制作工艺，由世界烹饪大师屈浩先生领衔研发。坚守纯天然、0添加的良心品质深得消费者青睐，发展至今成为粥类的引领品牌。是2008年奥运会和2013年园博会指定餐饮服务商。",
    "supports": [
      {
        "type": 0,
        "description": "在线支付满28减5"
      },
      {
        "type": 1,
        "description": "VC无限橙果汁全场8折"
      },
      {
        "type": 2,
        "description": "单人精彩套餐"
      },
      {
        "type": 3,
        "description": "该商家支持发票,请下单写好发票抬头"
      },
      {
        "type": 4,
        "description": "已加入“外卖保”计划,食品安全保障"
      }
    ],
    "avatar": "http://static.galileo.xiaojukeji.com/static/tms/seller_avatar_256px.jpg",
    "pics": [
      "http://fuss10.elemecdn.com/8/71/c5cf5715740998d5040dda6e66abfjpeg.jpeg?imageView2/1/w/180/h/180",
      "http://fuss10.elemecdn.com/b/6c/75bd250e5ba69868f3b1178afbda3jpeg.jpeg?imageView2/1/w/180/h/180",
      "http://fuss10.elemecdn.com/f/96/3d608c5811bc2d902fc9ab9a5baa7jpeg.jpeg?imageView2/1/w/180/h/180",
      "http://fuss10.elemecdn.com/6/ad/779f8620ff49f701cd4c58f6448b6jpeg.jpeg?imageView2/1/w/180/h/180"
    ],
    "infos": [
      "该商家支持发票,请下单写好发票抬头",
      "品类:其他菜系,包子粥店",
      "北京市昌平区回龙观西大街龙观置业大厦底商B座102单元1340",
      "营业时间:10:00-20:30"
    ]
  }}
```

PS：

**所有的修改配置都需要重新启动运行命令的：npm run dev才能生效（很重要，否则无法请求到数据）**

# vue常用介绍

### v-bind指令

 v-bind指令可以在后面带一个参数，中间用冒号隔开，这个参数一般是HTML的属性，比如v-bind:class ,可缩写为:class，这个class和原来的class 并不冲突。

## v-if指令

`v-if`是条件渲染指令，它根据表达式的真假来删除和插入元素，它的基本语法如下：

```
v-if="expression"
```

expression是一个返回bool值的表达式，表达式可以是一个bool属性，也可以是一个返回bool的运算式。例如：

```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title></title>
    </head>
    <body>
        <div id="app">
            <h1>Hello, Vue.js!</h1>
            <h1 v-if="yes">Yes!</h1>
            <h1 v-if="no">No!</h1>
            <h1 v-if="age >= 25">Age: {{ age }}</h1>
            <h1 v-if="name.indexOf('jack') >= 0">Name: {{ name }}</h1>
        </div>
    </body>
    <script src="js/vue.js"></script>
    <script>
        
        var vm = new Vue({
            el: '#app',
            data: {
                yes: true,
                no: false,
                age: 28,
                name: 'keepfool'
            }
        })
    </script>
</html>
```

**注意：**yes, no, age, name这4个变量都来源于Vue实例选项对象的data属性。

[![image](https://images2015.cnblogs.com/blog/341820/201606/341820-20160627065314546-1211050706.png)](http://images2015.cnblogs.com/blog/341820/201606/341820-20160627065313781-1005102718.png)

这段代码使用了4个表达式：

- 数据的`yes`属性为true，所以"Yes!"会被输出；
- 数据的`no`属性为false，所以"No!"不会被输出；
- 运算式`age >= 25`返回true，所以"Age: 28"会被输出；
- 运算式`name.indexOf('jack') >= 0`返回false，所以"Name: keepfool"不会被输出。

**注意：**v-if指令是根据条件表达式的值来执行**元素的插入或者删除行为。**

这一点可以从渲染的HTML源代码看出来，面上只渲染了3个<h1>元素，`v-if`值为false的<h1>元素没有渲染到HTML。

[![image](https://images2015.cnblogs.com/blog/341820/201606/341820-20160627065316265-161676773.png)](http://images2015.cnblogs.com/blog/341820/201606/341820-20160627065315515-1776406933.png)

为了再次验证这一点，可以在Chrome控制台更改age属性，使得表达式`age >= 25`的值为false，可以看到`<h1>Age: 28</h1>`元素被删除了。

[![3](https://images2015.cnblogs.com/blog/341820/201606/341820-20160627065319406-1162614113.gif)](http://images2015.cnblogs.com/blog/341820/201606/341820-20160627065317577-1183006666.gif)

age是定义在选项对象的data属性中的，为什么Vue实例可以直接访问它呢？
这是因为**每个Vue实例都会代理其选项对象里的data属性。**

## v-show指令

`v-show`也是条件渲染指令，和v-if指令不同的是，使用`v-show`指令的元素始终会被渲染到HTML，它只是简单地为元素设置CSS的style属性。

```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title></title>
    </head>
    <body>
        <div id="app">
            <h1>Hello, Vue.js!</h1>
            <h1 v-show="yes">Yes!</h1>
            <h1 v-show="no">No!</h1>
            <h1 v-show="age >= 25">Age: {{ age }}</h1>
            <h1 v-show="name.indexOf('jack') >= 0">Name: {{ name }}</h1>
        </div>
    </body>
    <script src="js/vue.js"></script>
    <script>
        
        var vm = new Vue({
            el: '#app',
            data: {
                yes: true,
                no: false,
                age: 28,
                name: 'keepfool'
            }
        })
    </script>
</html>
```

## [![image](https://images2015.cnblogs.com/blog/341820/201606/341820-20160627065321359-1780927154.png)](http://images2015.cnblogs.com/blog/341820/201606/341820-20160627065320577-322007545.png)

在Chrome控制台更改age属性，使得表达式`age >= 25`的值为false，可以看到`<h1>Age: 24</h1>`元素被设置了style="display:none"样式。

[![4](https://images2015.cnblogs.com/blog/341820/201606/341820-20160627065324343-1072339483.gif)](http://images2015.cnblogs.com/blog/341820/201606/341820-20160627065322656-1570128969.gif)

## v-else指令

可以用v-else指令为v-if或v-show添加一个“else块”。v-else元素必须立即跟在v-if或v-show元素的后面——否则它不能被识别。

<!DOCTYPE html>
<html>

    <head>
        <meta charset="UTF-8">
        <title></title>
    </head>
    <body>
        <div id="app">
            <h1 v-if="age >= 25">Age: {{ age }}</h1>
            <h1 v-else>Name: {{ name }}</h1>
            <h1>---------------------分割线---------------------</h1>
            <h1 v-show="name.indexOf('keep') >= 0">Name: {{ name }}</h1>
            <h1 v-else>Sex: {{ sex }}</h1>
        </div>
    </body>
    <script src="js/vue.js"></script>
    <script>
        var vm = new Vue({
            el: '#app',
            data: {
                age: 28,
                name: 'keepfool',
                sex: 'Male'
            }
        })
    </script>
</html>

v-else元素是否渲染在HTML中，取决于前面使用的是v-if还是v-show指令。
这段代码中v-if为true，后面的v-else不会渲染到HTML；v-show为tue，但是后面的v-else仍然渲染到HTML了。



## v-for指令

v-for指令基于一个数组渲染一个列表，它和JavaScript的遍历语法相似：

v-for="item in items"

items是一个数组，item是当前被遍历的数组元素。
隐藏代码

<!DOCTYPE html>
<html>

    <head>
        <meta charset="UTF-8">
        <title></title>
        <link rel="stylesheet" href="styles/demo.css" />
    </head>
    
    <body>
        <div id="app">
            <table>
                <thead>
                    <tr>
                        <th>Name</th>
                        <th>Age</th>
                        <th>Sex</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="person in people">
                        <td>{{ person.name  }}</td>
                        <td>{{ person.age  }}</td>
                        <td>{{ person.sex  }}</td>
                    </tr>
                </tbody>
            </table>
        </div>
    </body>
    <script src="js/vue.js"></script>
    <script>
        var vm = new Vue({
            el: '#app',
            data: {
                people: [{
                    name: 'Jack',
                    age: 30,
                    sex: 'Male'
                }, {
                    name: 'Bill',
                    age: 26,
                    sex: 'Male'
                }, {
                    name: 'Tracy',
                    age: 22,
                    sex: 'Female'
                }, {
                    name: 'Chris',
                    age: 36,
                    sex: 'Male'
                }]
            }
        })
    </script>

</html>

我们在选项对象的data属性中定义了一个people数组，然后在#app元素内使用v-for遍历people数组，输出每个person对象的姓名、年龄和性别。

## vue的computed怎么使用？

在模板中表达式非常便利，但是它们实际上只用于简单的操作。模板是为了描述视图的结构。在模板中放入太多的逻辑会让模板过重且难以维护。这就是为什么 Vue.js 将绑定表达式限制为一个表达式。如果需要多于一个表达式的逻辑，应当使用**计算属性** 。

```
<div id="example">
  a={{ a }}, b={{ b }}
</div>
```

```
var vm = new Vue({
  el: '#example',
  data: {
    a: 1
  },
  computed: {
    // 一个计算属性的 getter
    b: function () {
      // `this` 指向 vm 实例
      return this.a + 1
    }
  }
})
```

结果：

```
{% raw %}
<div id="example" class="demo">
  a={{ a }}, b={{ b }}
</div>
<script>
var vm = new Vue({
  el: '#example',
  data: {
    a: 1
  },
  computed: {
    b: function () {
      return this.a + 1
    }
  }
})
</script>
{% endraw %}
```

这里我们声明了一个计算属性 `b`。我们提供的函数将用作属性 `vm.b`的 getter。

```
console.log(vm.b) // -> 2
vm.a = 2
console.log(vm.b) // -> 3
```

你可以打开浏览器的控制台，修改例子的 vm。`vm.b` 的值始终取决于 `vm.a` 的值。

你可以像绑定普通属性一样在模板中绑定计算属性。Vue 知道 `vm.b` 依赖于 `vm.a`，因此当 `vm.a` 发生改变时，依赖于 `vm.b` 的绑定也会更新。而且最妙的是我们是声明式地创建这种依赖关系：计算属性的 getter 是干净无副作用的，因此也是易于测试和理解的。

## 计算属性 vs. $watch

Vue.js 提供了一个方法 `$watch`，它用于观察 Vue 实例上的数据变动。当一些数据需要根据其它数据变化时， `$watch` 很诱人 —— 特别是如果你来自 AngularJS。不过，通常更好的办法是使用计算属性而不是一个命令式的 `$watch` 回调。考虑下面例子：

```
<div id="demo">{{fullName}}</div>
```

```
var vm = new Vue({
  data: {
    firstName: 'Foo',
    lastName: 'Bar',
    fullName: 'Foo Bar'
  }
})

vm.$watch('firstName', function (val) {
  this.fullName = val + ' ' + this.lastName
})

vm.$watch('lastName', function (val) {
  this.fullName = this.firstName + ' ' + val
})
```

上面代码是命令式的重复的。跟计算属性对比会更好：

```
var vm = new Vue({
  data: {
    firstName: 'Foo',
    lastName: 'Bar'
  },
  computed: {
    fullName: function () {
      return this.firstName + ' ' + this.lastName
    }
  }
})
```

## 计算 setter

计算属性默认只是 getter，不过在需要时你也可以提供一个 setter：

```
// ...
computed: {
  fullName: {
    // getter
    get: function () {
      return this.firstName + ' ' + this.lastName
    },
    // setter
    set: function (newValue) {
      var names = newValue.split(' ')
      this.firstName = names[0]
      this.lastName = names[names.length - 1]
    }
  }
}
// ...
```

现在在调用 `vm.fullName = 'John Doe'` 时，setter 会被调用，`vm.firstName` 和 `vm.lastName` 也会有相应更新。

## 条件渲染

### v-if

在字符串模板中，如 Handlebars，我们得像这样写一个条件块：

```
<!-- Handlebars 模板 -->
{{#if ok}}
  <h1>Yes</h1>
{{/if}}
```

在 Vue.js，我们使用 `v-if` 指令实现同样的功能：

```
<h1 v-if="ok">Yes</h1>
```

也可以用 `v-else` 添加一个 "else" 块：

```
<h1 v-if="ok">Yes</h1>
<h1 v-else>No</h1>
```

## template v-if

因为 `v-if` 是一个指令，需要将它添加到一个元素上。但是如果我们想切换多个元素呢？此时我们可以把一个 `<template>` 元素当做包装元素，并在上面使用 `v-if`，最终的渲染结果不会包含它。

```
<template v-if="ok">
  <h1>Title</h1>
  <p>Paragraph 1</p>
  <p>Paragraph 2</p>
</template>
```

## v-show

另一个根据条件展示元素的选项是 `v-show` 指令。用法大体上一样：

```
<h1 v-show="ok">Hello!</h1>
```

不同的是有 `v-show` 的元素会始终渲染并保持在 DOM 中。`v-show` 是简单的切换元素的 CSS 属性 `display`。

注意 `v-show` 不支持 `<template>` 语法。

v-else

可以用 v-else 指令给 v-if 或 v-show 添加一个 "else 块"：

<div v-if="Math.random() > 0.5">
  Sorry
</div>
<div v-else>
  Not sorry
</div>

v-else 元素必须立即跟在 v-if 或 v-show 元素的后面——否则它不能被识别。
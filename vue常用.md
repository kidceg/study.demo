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
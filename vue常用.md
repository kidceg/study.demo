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
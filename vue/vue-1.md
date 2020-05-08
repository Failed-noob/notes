### vue 初步:

​	简介:
​		vue 是一套构建用户界面的渐进式框架. 可以自底向上逐层应用 MVVM响应式编程模型,避免直接操作DOM 降低DOM操作的复杂程度.



模块化:

​	模块化就是有组织地把一个大文件拆成独立并互相依赖的多个小模块。



### 模块化的好处

- 避免命名冲突(减少命名空间污染)
- 更好的分离, 按需加载
- 更高复用性
- 高可维护性

module.exports  || exports  用着两货暴露出模块 再另一个文件中用require 引入该模块;



组件化:

​	*组件化*是指解耦复杂系统时将多个功能模块拆分、重组的过程，有多种属性、状态反映其内部特性。 

​	说白了 上面的模块化 和 组件化 没多大区别.   组件化  也是有更强的复用性之类的....



先来看看很基础的一个例子:



```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <script src="../vue.js/vue.min.js"></script>
    <title>Document</title>
    <style>
        .eg {
            color: pink;
        }
    </style>
</head>
<body>
    <div id="app" :title='meg' v-if='see' :class='{eg:okk}'>
        {{meg}}
    </div>
    <script>
        var vm= new Vue({
            el: "#app",
            data: {
                meg: 'vue实例',
                see:true,
                okk:true
            }
        })    
        console.log(Vue.prototype)
        console.log(vm)
    </script>
</body>
</html>
```

上面的这个class 绑定 就有点特殊  希望注意

怎么引入这个js文件相信 不用多bb了   将vm 这个构造函数 打印在控制台  里面肯定是 这个实例对象的方法和属性 但现在 看的还是一脸懵;





再vue中 有一些缩写   

v-bind <=>  :  (绑定属性)

v-on:click  <=> @click (绑定事件)
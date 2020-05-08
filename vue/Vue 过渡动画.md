### Vue 过渡动画







 v-enter定义进入过渡开始状态,在元素被插入之前生效

   通俗的讲: 

   就像下面的进来之前还在 -100%的视图外;这个玩意在 [v-enter-to]路由完全进入之后就删除了

   v-enter-active 这是一个时间段 

   在组件从出现到出现完成的过程中 这个类可以被用来定义进入过度的过程时间 就是在这个类里加一个动画;

   v-enter-to 进入完成 此时的一个状态点 此时元素处于一个什么状态[此时v-enter 被移除了];

   v-leave 准备离开的一个状态 在这个点的状态

   v-leave-active 这个就跟英语中的正在进行时一样 be going

​    与上面的v-enter-active 差不多

  v-leave-to 离开完成 在这个时间点的状态;

![](D:\QQ截图\vue 过渡过程.png)





下列例子 来复习一下:



css中 transition 需要 用户做出某种行为时 才会触发   例如 :  hover   checked focus  ...

而 animation 需要先创建一个动画过程后 才能运行  在这里用transition  我真的有点懵逼 





v-if  指令 当为false 时 页面上没有显示  此时页面元素中没有创建该元素;

为true时 vue指令会在页面中创建 该元素;    而 v - show  为false时 该元素有一个属性 display :none 在起作用;

而 为true display 就失效了

```html

<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <!-- <link rel="stylesheet" href="../lib/bootstrap.css"> -->
    <script src="../vue.js/vue.min.js"></script>
    <script src="../vue.js/vue-resource.js"></script>
    <style>
        .v-enter,
        .v-leave-to {
            /* opacity: 0; */
            color: pink;
        }
        .v-enter-active,
        .v-enter-active {
            transition: all 2s ease-in-out ;
        }
    </style>
</head>
<body>
    <div id="app">
        <input type="button" value="v / appear" @click='v()'>
        <transition >
            <p v-if='tab'>我是一段普通的段落文字</p>
        </transition>
    </div>

<script>
 var vm = new Vue({
  el:'#app',
  data:{
      tab:false
  },
  methods:{
      v(){
          this.tab=!this.tab
      }
  }
 }) ;
 </script>
</body>
</html>


// 用animation 

<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <!-- <link rel="stylesheet" href="../lib/bootstrap.css"> -->
    <script src="../vue.js/vue.min.js"></script>
    <script src="../vue.js/vue-resource.js"></script>
    <style>
        /* .v-enter,
        .v-leave-to {
            opacity: 0;
        } */
        .v-enter-active {
            animation: bounce-in 2s ease-in-out ;
        }
        .v-leave-active {
           animation: bounce-in  reverse 2s ease-in-out ;
        }
        @keyframes bounce-in {
            0% {
                transform: scale(0);
            }
            50% {
                transform: scale(2);
            }
            100% {
                transform: scale(1);
            }
        }
    </style>
</head>
<body>
    <div id="app">
        <input type="button" value="v / appear" @click='v()'>
        <transition >
            <p v-if='tab'>我是一段普通的段落文字</p>
        </transition>
    </div>

<script>
 var vm = new Vue({
  el:'#app',
  data:{
      tab:false
  },
  methods:{
      v(){
          this.tab=!this.tab
      }
  }
 }) ;
 </script>
</body>
</html>


// 用 第三方库
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <!-- <link rel="stylesheet" href="../lib/bootstrap.css"> -->
    <script src="../vue.js/vue.min.js"></script>
    <script src="../vue.js/vue-resource.js"></script>
    <link rel="stylesheet" href="../jq&bootstrap&axios/animate.css">
    <style>
        /* .v-enter,
        .v-leave-to {
            opacity: 0;
        } */

        /* .v-enter-active {
            animation: bounce-in 2s ease-in-out ;
        }
        .v-leave-active {
           animation: bounce-in  reverse 2s ease-in-out ;
        } */

        /* @keyframes bounce-in {
            0% {
                transform: scale(0);
            }
            50% {
                transform: scale(2);
            }
            100% {
                transform: scale(1);
            }
        } */
    </style>
</head>
<body>
    <div id="app">
        <input type="button" value="v / appear" @click='v()'>
        <transition name='tab' enter-active-class="animated tada" leave-active-class="animated bounceOutRight">  
            <p v-if='tab'>我是一段普通的段落文字</p>
        </transition>
    </div>

<script>
 var vm = new Vue({
  el:'#app',
  data:{
      tab:false
  },
  methods:{
      v(){
          this.tab=!this.tab
      }
  }
 }) ;
 </script>
</body>
</html>
```



对于 上面的类名 也可以改成 自定义的 只需要在 给transition 标签加上一个 name 属性 此时 那个类名就可以 不用    **v-**    用 你自定义的name属性的 名称;



  据现在所理解  这是专门为第三方库而 弄的几个 属性

- `enter-class`     v-enter 为刚进入的状态 设置的动画的类名
- `enter-active-class `  跟 enter-active 一样的时间 这段时间所设置的类名
- `enter-to-class` (2.1.8+)       enter-to
- `leave-class`   v-leave
- `leave-active-class`    v-leave-active
- `leave-to-class` (2.1.8+)  v-leave-to 


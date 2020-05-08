### Vue组件





组件的名称  可以是  xxxxx-yyyy (在我的垃圾电脑中 这种用 vscode 无法呈现 但是用下划线可以  )   亦可以是驼峰命名法   QsdfsdHsdfsdf 此类的 

​		就个人看法 就是将整个页面 分成几个小的部分 就比如说一个页面的header部分 我就可以写一个组件 将整个header完全展现出来 ;大概i着这样理解;



定义:

可复用的Vue实例  但是组件中不需要 el 属性 不需要挂载目标属性;



组件也分为全局组件 和 局部组件 ( **局部注册的组件 在其子组件中不可用**);

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script src="../vue.js/vue.min.js"></script>
    <script src="../vue.js/vue-resource.js"></script>
</head>
<body>
<div id="app">
    <one></one><one></one>
    <two></two>

    <field></field>
</div>
<div id="demo" style="background: red; width: 100px; height: 200px;">
    <one></one>
    {{msg}}
</div>
<script>
// 定义全局组件 组件是可以重复使用的
Vue.component('one',{
    template:'<mark>我是第一个组件 而且还是黄色的</mark>'
})
Vue.component('two',{
    template:'<mark>我是第二个组件 而且还是黄色的</mark>'
})

//定义局部组件 需要在vue实例中声明这一组件;
let field =  {
    template: '<p>我是一个局部组件</p>'
}

 var vm = new Vue({
  el:'#app',
  data:{},
  methods:{},
 components:{
    field
 }

 }) ;

var vm1= new Vue({
    el: '#demo',
    data:{
        msg:'hello'
    }
})
 </script>
</body>
</html>

```



在这里多加一句   对于组件的 data而言  这个data必须是一个函数 如下: 

```javascript
data : function (){
    return {
        
    }
}
```





#### 组件之间的通信



父 => 子



通过 props 属性 

```vue
// 父
<template>
  <div id="app">

      <img alt="Vue logo" src="./assets/logo.png">
      <HelloWorld msg="父组件中传过来的值"/>
      <VueTest :advise =" mes"/>
      <Child  @listenChildEvent="getData"></Child>
      <input type="button" value="chilren" @click="hh">
      <hr /><hr />

  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import VueTest from './components/test.vue'
import Child from './components/child.vue'


export default {
  name: 'App',
  data:function(){
    return {
      mes:'hahhahahahahhaafdsdsfdsafsf'
    }
  },
  methods: {
    getData(data){
      console.log(data)
    },
    hh(){
      console.log(this)
    }
  },
  components: {
    HelloWorld,
    VueTest,
    Child
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>


// 子

<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String 
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>

```



子 = > 父



```vue
// 父
<template>
  <div id="app">

      <img alt="Vue logo" src="./assets/logo.png">
      <HelloWorld msg="父组件中传过来的值"/>
      <VueTest :advise =" mes"/>
      <Child  @listenChildEvent="getData"></Child>
      <input type="button" value="chilren" @click="hh">
      <hr /><hr />

  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import VueTest from './components/test.vue'
import Child from './components/child.vue'


export default {
  name: 'App',
  data:function(){
    return {
      mes:'hahhahahahahhaafdsdsfdsafsf'
    }
  },
  methods: {
    getData(data){
      console.log(data)
    },
    hh(){
      console.log(this)
    }
  },
  components: {
    HelloWorld,
    VueTest,
    Child
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>


//子

<template>        
    <div>
        <input type="button" value="子组件传给父组件" @click='childDeliverFather'>
    </div>
</template>
<script>
    export default {
        name:'Child',
        
        methods: {
            childDeliverFather(){
                this.$emit("listenChildEvent",'These words from the child')
            }
        },
    }
</script>
<style scope lang="">
    
</style>
```



2.2 vue实例 新增的属性;

provide / inject  这两货 是可以 由 父亲 直接 传到 孙子 曾孙 重孙 ......

就表面意思来讲 provide 就是提供   inject  就是接受    

**父组件用 provide 提供数据  子组件用 inject 接受数据  [ 就个人见解 : provide 是 像 data一样的 对象 ;   而 inject  是个 数组 ]  看下面代码吧 **



```vue
//app .vue

<template>
  <div id="app">

      <img alt="Vue logo" src="./assets/logo.png">
      <HelloWorld msg="父组件中传过来的值"/>
      <VueTest :advise =" mes"/>
      <Child  @listenChildEvent="getData"></Child>
      <input type="button" value="chilren" @click="hh">
      <hr /><hr />
      <InjectChild />

  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import VueTest from './components/test.vue'
import Child from './components/child.vue'
import InjectChild from './components/inject-child.vue'


export default {
  name: 'App',
  data:function(){
    return {
      mes:'hahhahahahahhaafdsdsfdsafsf'
    }
  },
  provide: {
    information: 'context'
  },
  methods: {
    getData(data){
      console.log(data)
    },
    hh(){
      console.log(this)
    }
  },
  components: {
    HelloWorld,
    VueTest,
    Child,
    InjectChild
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

//injectChild

<template>
    <div>
        <injecgrandson />
        <p>{{msg}}</p>
    </div>
</template>
<script>
import injecgrandson from './inject-grandson.vue'
export default {
    name:'InjectChild',
    data(){
        return {
            msg:this.information
        }
    },
    provide: {
        infor: 'hahahahaha'
    },
    inject:['information'],
    components: {
        injecgrandson
    }
}
</script>
<style scoped>
    
</style>

// inject grandson 
<template>
    <div>
        <p>I'm grandson</p>
        <mark>{{mes}}</mark>
        <strong>{{mssg}}</strong>
    </div>
</template>
<script>
export default {
    name:'injec-grandson',
    data(){
        return {
            mes: this.information,
            mssg: this.infor
        }
    },
    
    inject:[['information'],['infor']]

}
</script>
<style scoped>
    
</style>

```



### **动态组件:**

进行组件之间的切换,即动态组件;



动态组件通过Vue的<component>元素 加一个 is 属性来完成 [具体的 我真的不是很懂]

看例子吧:

```vue
//app.vue

<template>
  <div id="app">

    <Dyna @toggle="change"> </Dyna>
    <component :is = "comName"></component>
  </div>
</template>

<script>
import Dyna from "./components/dynamicComponent"
import first from "./components/firstSon"
import second from "./components/secondSon"

export default {
  name: 'App',
  data(){
    return {
      comName:""
    }
  },
  components: {
    Dyna,
    first,
    second
  },
  methods:{
    change(data){
        this.comName = data
    }
  }
}
</script>

<style scoped>
  #app:before {
    content: '';
    display: block;
    clear: both;
  }
#app {
  height: 100px;
  border: 2px solid pink;
}
</style>

```



上面

在上面的component元素中 当is的属性为哪一个组件时 在页面中就渲染的是哪一个组件;



### **异步组件:**

```JavaScript
Vue.component('async-example', function (resolve, reject) {
  setTimeout(function () {
    // 向 `resolve` 回调传递组件定义
    resolve({
      template: '<div>I am async!</div>'
    })
  }, 1000)
})
```


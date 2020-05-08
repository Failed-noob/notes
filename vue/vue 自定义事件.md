### vue 自定义事件



根据自己按照官网敲得 代码  先来看看 如何定义自定义事件

 

借用 数学中的术语  当且仅当   vue实例 例如 Vm.$emit ( " 自定义事件名")  此时  自定义事件 就已经声明了  然后直接用 类似 

```
@click
```



给自定义事件 看代码吧  有点说不清楚了;{  就比如 子 =>  父  组件之间的通信

```vue
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

//父
<template>
  <div id="app" >

      <img alt="Vue logo" src="./assets/logo.png">
      <hello_world msg="父组件中传过来的值"/>
      <VueTest :advise =" mes"/>
      <Child  @listenChildEvent="getData"></Child>
      <input type="button" value="chilren" @click="hh">
      <hr /><hr />
      <InjectChild />
      <br /><hr />
      <div :style="{ fontSize: postFontSize + 'em' }">
          <BlogPost :items='posts' @enlargeContext="postFontSize += 0.1"/>
      </div>
      
  </div>
</template>

<script>
import hello_world from './components/HelloWorld.vue'
import VueTest from './components/test.vue'
import Child from './components/child.vue'
import InjectChild from './components/inject-child.vue'
import BlogPost from './components/blog-post.vue'


export default {
  name: 'App',
  data:function(){
    return {
      mes:'hahhahahahahhaafdsdsfdsafsf',
      posts: [
        { id: 1, title: 'My journey with Vue' },
        { id: 2, title: 'Blogging with Vue' },
        { id: 3, title: 'Why Vue is so fun' }
      ],
      postFontSize:.6
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
    hello_world,
    VueTest,
    Child,
    InjectChild,
    BlogPost
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

```


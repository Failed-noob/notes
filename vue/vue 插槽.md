### vue 插槽<https://www.cnblogs.com/chinabin1993/p/9115396.html>



上面的这个网址里面讲的很好 简洁 



本来组件 显示在页面上就完了  这是之前的理解;但有了插槽,

比如  组件<Haha></Haha>  这样写了就出现该出现的内容了  一直有这种想法 跟html 的标签差不多 却屁都不能装   这时 插槽就让我舒服多了   在组件内写 <slot></slot> 这么一对标签 你在这组件中间 想写啥写啥



```vue
//子组件

<template>
    <div>
        <button type="button">
            <slot></slot> <!-- 在slot标签中填入想要默认的名称 -->
        </button>
    </div>
</template>
<script>
export default {
    name:"sl",
    data(){
        return {
           items:{
            "name":"tom",
            "gender":"male"

           }
        }
    }
}
</script>
<style scoped> 
    
</style>

//父组件

<template>
  <div id="app" >

      <img alt="Vue logo" src="./assets/logo.png">
      <hello_world msg="父组件中传过来的值"/>
      <Haha :advise =" mes"/>
      <Child  @listenChildEvent="getData"></Child>
      <input type="button" value="chilren" @click="hh">
      <hr /><hr />
      <InjectChild />
      <br /><hr />
      <div :style="{ fontSize: postFontSize + 'em' }">
          <BlogPost :items='posts' @enlargeContext="postFontSize += 0.1"/>
      </div>
      <hr />

      <!-- 下面的 button 就是在组件中声明了 <slot></slot>-->
      <Sl>button</Sl>
       <!-- <router-view></router-view> -->
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import Haha from './components/Haha.vue'
import Child from './components/child.vue'
import InjectChild from './components/inject-child.vue'
import BlogPost from './components/blog-post.vue'
import Sl from './components/slot'


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
    HelloWorld,
    Haha,
    Child,
    InjectChild,
    BlogPost,
    Sl
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





作用域插槽: 插槽内容 [ 插槽是放在父组件中的 ] 能够访问子组件中才有的数据



如何才能在父组件中访问到子组件中的数据 ====>   只要将上面的代码稍微改一下就好;

```vue
// 子组件
  <slot :items='items'>{{items.name}}</slot>  
//就该这点 在未加这个items属性的时候 仍然访问不到 加了之后然后在负组件中做出如下操作

//父组件  在 2.6 的版本之前  用的是 slot-scope (但已弃用)
	<Sl>
        <template v-slot='gg'>
          {{gg.items.gender}}
        </template>
      </Sl>

```


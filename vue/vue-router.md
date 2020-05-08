## vue-router 



vue-router   vue.js 官方的路由管理器;

```markdown
功能:

嵌套的路由/视图表
模块化的、基于组件的路由配置
路由参数、查询、通配符
基于 Vue.js 过渡系统的视图过渡效果
细粒度的导航控制
带有自动激活的 CSS class 的链接
HTML5 历史模式或 hash 模式，在 IE9 中自动降级
自定义的滚动条行为
```

### **最基础的路由:**

```javascript
//main.js
import Vue from 'vue'
import App from './App.vue'
import store from './store'
import VRouter from 'vue-router'
import One from './components/routerPageOne'
import Two from './components/routerPageTwo'

Vue.use(VRouter)
Vue.config.productionTip = false

let routes = [
  {
    path:'/',
    component: One
  },
  {
    path:'/two',
    component: Two
  }
];

const router = new VRouter({
  routes
})


new Vue({
  router,
  store,
  render: h => h(App)
}).$mount('#app')

//app.vue
<template>
  <div id="app">

    <!--<Dyna @toggle="change"> </Dyna>-->
    <!--<component :is = "comName"></component>-->
    <router-link to="/">routerOne</router-link>
    <router-link to="/two">routerTwo</router-link>
    <router-view />
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

动态路由匹配:

​	一个“路径参数”使用冒号 `:` 标记。当匹配到一个路由时，参数值会被设置到 `this.$route.params`，可以在每个组件内使用。于是，我们可以更新 `User` 的模板，输出当前用户的 ID：

```markdown
const User = {
  template: '<div>User</div>'
}

const router = new VueRouter({
  routes: [
    // 动态路径参数 以冒号开头
    { path: '/user/:id', component: User }
  ]
})


const User = {
  template: '<div>User {{ $route.params.id }}</div>'
}
```



复杂的先不说 先来看看 路由的重定向 

```vue
const router = new VueRouter({
  routes: [
    { path: '/a', redirect: '/b' }, //本来时a 由于后面有一个redirect 所以就指向 路由 b 了

// 重定向的目标也可以是 命名的路由
	{path:'/c',redirect: {name: "foo"}}
  ]
})

//是一个方法，动态返回重定向目标：
const router = new VueRouter({
  routes: [
    { path: '/a', redirect: to => {
      // 方法接收 目标路由 作为参数
      // return 重定向的 字符串路径/路径对象
    }}
  ]
})
```


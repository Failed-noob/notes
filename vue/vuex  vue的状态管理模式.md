### vuex : vue的状态管理模式



**vuex**: 它采用集中式存储管理应用的所有组建的状态,并以相应的规则保证状态以一种可预测的方式发生变化

​		在中大型单页面应用 推荐用vuex  如果应用不大 建议用一些简单的store 模式







```JavaScript

var store = {
  debug: true,
  state: {
    message: 'Hello!'
  },
  setMessageAction (newValue) {
    if (this.debug) console.log('setMessageAction triggered with', newValue)
    this.state.message = newValue
  },
  clearMessageAction () {
    if (this.debug) console.log('clearMessageAction triggered')
    this.state.message = ''
  }
}


--------------------------------------------
    var vmA = new Vue({
  data: {
    privateState: {},
    sharedState: store.state
  }
})

var vmB = new Vue({
  data: {
    privateState: {},
    sharedState: store.state
  }
})
```

 

从上面代码来看 一切属性都在 store 这个对象里面  所以store 就是Vue的应用核心



这个store ( **就现在的自己的看法 store 对象就可以看成 Vuex**) 和 单纯的全局对象是有区别的:



**vuex的状态存储是响应式的 .当vue组件从store中读取状态的时候 若store 的状态发生变化 那么相应的组件也会发生变化**;



**重要的vuex中的 state 是无法直接改变的 .改变state中的状态的唯一途径 就是显式提交commit **



​	



**vuex 的五个重要属性:**

1. ​  State
2.  Getter
3.  Mutation
4.  Action
5.  Module



我们通过提交 mutation 的方式，而非直接改变 `store.state.count`，是因为我们想要更明确地追踪到状态的变化 这是约定 。

```javascript
//store.js
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)


//TYPES
const types = {
  SET_LOCATION:"SET_LOCATION",
  SET_ADDRESS:"SET_ADDRESS"

}

//state
const state = {
  number:12,
  location: {},
  address:""
}

//getters 
const getters = {
  location:state => state.location,
  address:state=> state.address
}

//Mutations
const mutations = {
  [types.SET_LOCATION](state,location){
    if(location){
      state.location = location;
    }else {
      state.location = null;
    }
  },
  [types.SET_ADDRESS](state,address){
    if(address){
      state.address = address;
    }else {
      state.address = null;
    }
  }
},

//actions
  actions = {
  setLocation :({commit},location)=>{
    commit(types.SET_LOCATION,location)
  },
  setAddress :({commit},address)=>{
    commit(types.SET_ADDRESS,address)
  }
}
export default new Vuex.Store({
 state,
 getters,
 mutations,
 actions
})

// home.vue
<template>
<!-- home -->
    <div class="home">
        home
        {{num}}
  		{{number}}
    </div>
</template>
<script>
// import {mapState} from "vuex"
export default {
    name:"home",
    data(){
      return{
        
      }
    },
    computed:{
      num(){
        return this.$store.state.number
      }
        下面的这种是对象展开运算符 
        //...mapState({
        //num: state=>state.number
      //})
        
        //number 是方法名
         ...mapGetters(['number'])
    }
}
</script>
<style scoped>
    .index{
        width: 100%;
        height: 100%;
        color: white;
        background: pink;
    }
</style>
```



在任意组件都可以 通过 computed 属性将 想要的数据return 然后直接用  这里还有一个mapstate 辅助函数  



上面的 state getters  不仅可以通过计算属性和mapState,mapGetters 来获取 还可以通过 $store.state     $store.getters 来获取到值 

当然 mutations 不同 它相当于一个事件的注册 需要用 commit 来触发方法  $store 也可以通过commit来触发   也可以通过 mapMutations 在methods 中来  然后通过事件来出来   但是看代码吧

```vue
//vuex 的store.js
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)
//state 
const state = {
  name:'dong_han',
  age: 18,
  turn:false,
  temprature:[]
};

//getters  store 中的 state 中派生出一些状态
const getters = {
nameToArray:function(state){
   return  state.name.split('_')
  },
age:function(state){
    return state.age++
  }
};

/*
Mutation 改变vuex中state中的状态唯一方法就是提
交 Mutation 
在Mutations中 的方法就像是注册事件 但是还没有调用 需要用commit来触发事件 
*/
const mutations = {
  increase:function(state,num){
    //变更state中的属性的状态
    state.age++;
    state.turn = !state.turn;
    state.temprature.push(++num)
  },
  decrease:function(state){
    //变更state中的属性的状态
    state.age--;
    state.turn = !state.turn;
    state.temprature=[]
  },
}

export default new Vuex.Store({
  state,
  getters,
  mutations
})



//home.vue
<template>
  <div class="home">
   hello__
    {{name}}
    {{nameToArray}}
  <p>{{age}}</p>
  <strong>status: {{turn}}</strong>
  <mark>{{temprature}}</mark>
  <button @click="$store.commit('increase',10)">按钮</button>
  <button @click="decrease">按钮二</button>
  </div>
</template>

<script>
// @ is an alias to /src
//

import { mapState,mapGetters,mapMutations } from "vuex"
export default {
  name: 'Home',
  computed:{
    //store中state的引用 或者用mapState辅助函数
    // name(){
    //   return this.$store.state.name
    // },
    ...mapState({
      name:state=>state.name,
      turn:state=>state.turn,
      age: state=>state.age,
      temprature:state=>state.temprature
    }),
    ...mapGetters(['nameToArray']),
   
  },
  created(){
    console.log(this.$store);
  },
  methods:{
    ...mapMutations(['decrease']),
    
  }
}
</script>

```



有时候 会用常量来作为mutation事件类型 :

```javascript
// mutation-types.js 
export const SOME_MUTATION = 'SOME_MUTATION' 
// store.js 
import Vuex from 'vuex' 
import { SOME_MUTATION } from './mutation-types' 
 
const store = new Vuex.Store({ 
 mutations: { 
    // 我们可以使用 ES2015 风格的计算属性命名功能来使用一个常量作为函数名 
    [SOME_MUTATION] (state) { 
      // mutate state 
    } 
  } 
}) 

```



##### 切记 mutation 必须是同步函数:





### Actions 

actions 处理异步操作 

 Action 提交的是 mutation，而不是直接变更状态。  Action 可以包含任意异步操作。 



```javascript
const store = new Vuex.Store({ 
  state: { 
    count: 0 
  }, 
  mutations: { 
    increment (state) { 
      state.count++ 
    } 
  }, 
  actions: { 
    increment (context) { 
      context.commit('increment') 
    } 
  } 
}) 
```



Action 函数 **接受一个与 store 实例具有相同方法和属性的 context 对象**，因此你 可以调用 context.commit 提交一个 mutation，或者通 过 context.state 和context.getters 来获取 state 和 getters 





在组件中分发 Action

```javascript
//store.js

import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)
//state 
const state = {
  name:'dong_han',
  age: 18,
  turn:false,
  temprature:[]
};

//getters  store 中的 state 中派生出一些状态
const getters = {
nameToArray:function(state){
   return  state.name.split('_')
  },
age:function(state){
    return state.age++
  }
};

/*
Mutation 改变vuex中state中的状态唯一方法就是提交 Mutation 
在Mutations中 的方法就像是注册事件 但是还没有调用 需要用commit来触发事件 
*/
const mutations = {
  increase:function(state,num){
    //变更state中的属性的状态
    state.age=state.temprature.length;
    state.turn = !state.turn;
    state.temprature.push(++num)
  },
  decrease:function(state){
    //变更state中的属性的状态
    state.age>0 ? state.age--: state.age=0;
    state.turn = !state.turn;
    state.temprature.pop()
  },
};

const actions = {
  upload({commit},num){
      //这个content 与 store实例 具有相同方法和属性
      commit('increase',num)
  }
}

export default new Vuex.Store({
  state,
  getters,
  mutations,
  actions
})

```



#### **还有一个  module 可以包含 state ,getters mutations actions ** 看下面的代码:

```JavaScript
const moduleA = { 
  state: { count: 0 }, 
  mutations: { 
    increment (state) { 
      // 这里的 `state` 对象是模块的局部状态 
      state.count++ 
    } 
  }, 
 
  getters: { 
    doubleCount (state) { 
      return state.count * 2 
    } 
  } 
} 


const moduleA = { 
  state: { ... }, 
  mutations: { ... }, 
  actions: { ... }, 
  getters: { ... } 
} 
 
const moduleB = { 
  state: { ... }, 
  mutations: { ... }, 
  actions: { ... } 
} 
 
const store = new Vuex.Store({ 
  modules: { 
    a: moduleA, 
    b: moduleB 
  } 
}) 
 
store.state.a // -> moduleA 的状态 
store.state.b // -> moduleB 的状态 
```




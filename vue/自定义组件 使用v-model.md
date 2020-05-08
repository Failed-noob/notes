### 自定义组件 使用v-model



组件之前 v-model 我一直以为 是input 元素之类的专属; 在 自定义组件上增加 v-model 是新增加的属性

```vue
//父组件
<template>
<div >
  <p>总数{{total}}</p>
  <button @click="addNumber">+1</button>
  <about-chil v-model="total"/>// 相当于 <about-chil :value="tatal"  @input="tatal=$event"/>
</div>
</template>
<script>
import AboutChil from './AboutChil.vue';
export default {
  data() {
    return {
      total: 8
    };
  },
  components: {
    AboutChil
  },
  methods:{
      addNumber(){
          this.total++
      }
  }

}

</script>


//子组件
<template>

<div>
  <p>我是儿子，父亲对我说： {{value}}</p>


    <input :value="total" @input="$emit('returnBack', $event.target.value)">//在一个input框中输入内容父子组件中的值也会改变

  <a href="javascript:;"  @click="returnBackFn">回应</a>
</div>
</template>
<script>

export default {

  props:['value'],//如果以这样的格式去写的话还想页面展示出来，必须是value

  methods: {

    returnBackFn() {

      this.$emit('input', 3);//此方法必须是input

    }

  }

}

</script>
```


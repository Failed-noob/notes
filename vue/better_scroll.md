#### **better-scroll 的安装和简单使用**

####  

### Attributes:

| 参数               | 说明                                                         | 类型              | 可选值                                                       | 默认值 |
| ------------------ | ------------------------------------------------------------ | ----------------- | ------------------------------------------------------------ | :----- |
| probeType          | 派发scroll事件的条件                                         | Number            | 1、2、3                                                      | 1      |
| click              | better-scroll 会派发一个 click 事件                          | Boolean           |                                                              | true   |
| listenScroll       | 是否监听滚动，开启后才能派发scroll事件                       | Boolean           |                                                              | false  |
| listenBeforeScroll | 是否监听滚动之前，开启后才能派发before-scroll-start事件      | Boolean           |                                                              | false  |
| scrollbar          | 这个配置可以开启滚动条。当设置为 true 或者是一个 Object 的时候，都会开启滚动条，默认是会 fade 的 | Boolean or Object | {fade: true},                                                | false  |
| pullDownRefresh    | 这个配置用于做下拉刷新功能。当设置为 true 或者是一个 Object 的时候，可以开启下拉刷新，可以配置顶部下拉的距离（threshold） 来决定刷新时机以及回弹停留的距离（stop） | Boolean or Object | {threshold: 90,stop: 40},                                    | false  |
| pullUpLoad         | 这个配置用于做上拉加载功能。当设置为 true 或者是一个 Object 的时候，可以开启上拉加载，可以配置离底部距离阈值（threshold）来决定开始加载的时机 | Boolean or Object | { threshold: 0, txt: { more: '加载更多',noMore:'没有更多数据了'} } | false  |
| startY             | 纵轴方向初始化位置                                           | Number            |                                                              | 0      |
| freeScroll         | 有些场景我们需要支持横向和纵向同时滚动，而不仅限制在某个方向，这个时候我们只要设置 freeScroll 为 true 即可 | Boolean           |                                                              | false  |
| options            | 可自行根据 better-scroll 官方文档 扩展参数 例：`:options="{stopPro` |                   |                                                              |        |

安装咱就不说了 npm cnpm yarn 安装都行 有什么用什么;

先说说在vue中的简单实用:



```markdown

// 点击旁边的 索引 跳转到相应的位置 我只碰到这个时候的应用
第一步还是要先初始化 better-scroll 这个对象 
 ScrollInit(){
      //设置之后 ref为goodlist的div 只能用指针拖动 滚轮失效 前提是将该div 设置为 overflow: hidden
      this.foodListScroll=new Bscroll (this.$refs.goodlist,{
        click:true
      })
    },
//首先 一般被点击的索引与 跳转到目标元素的索引值是一致的
1, 给被点击的元素注册一个点击事件 并将索引值作为形参传过去


```

还是看代码吧: [咱用语言解释的不是很通]

```vue
<template>
<!-- 详情页面中的点餐 -->
  <div class="order" v-if="shopDetails">
   <!-- 商家推荐 -->
   <div class="shopRecommend">
    <p class="title">{{shopDetails.recommend[0].name}}</p>
   <div class="content_box">
     <div class="recommend_content" v-for="(item,index) in shopDetails.recommend[0].items" :key="index">
      <div class="recommend_img">
        <img :src="item.image_path" alt="">
      </div>
      <div class="recommend_text">
        <p>{{item.name}}</p>
        <p>
          <span>评分{{item.rating}}</span>
          <span> 月售{{item.month_sales}}</span>
          <span> 好评率{{item.satisfy_rate}}%</span>
        </p>
      </div>
      <div class="price">
        <p>&yen; {{item.activity.fixed_price}}</p>
        <div>
          <QuantityControll :goodQuantity="item"/>
        </div>
      </div>
    </div>
   </div>
   </div>
   <!-- 商品分类 -->
  <div class="goodsclassify">
      <!--左侧导航-->
    <div class="goodmenu" ref="goodmenu">
      <ul>
        <li @click="selectMenu(index)" v-for="(item,index) in shopDetails.menu" :key="index">
          <img v-if="item.icon_url" :src="item.icon_url" alt="">
          <span>{{item.name}}</span>
        </li>
      </ul>
    </div>
  
    <!-- 右侧商品列表 -->
      <div class="goodlist" ref="goodlist">
        <ul>
          <li class="goodstitle" v-for="(item,index) in shopDetails.menu" :key="index">
            <!-- 商品的系列描述 -->
            <div class="category_tilte" ref="category_title">
              <span>{{item.name}}</span>
              <span v-if="item.description">{{item.description}}</span>
            </div>
            <!-- 商品信息 -->
            <div class="goodsInfo">
              <ul>
                <li class="goodsDtails" v-for="(food,i) in item.foods" :key="i">
                  <!-- 左侧图片 -->
                  <div class="goodsImg">
                    <img :src="food.image_path" alt="failed">
                  </div>
                  <!-- 右侧内容 -->
                  <div class="goodstext">
                    <h3>{{food.name}}</h3>
                    <p>{{food.description}}</p>
                    <p>
                      <span>月售{{food.month_sales}}份</span>
                      <span>好评率{{food.satisfy_rate}}%</span>
                    </p>
                    <div class="goodsPrice">
                      <p>&yen;{{food.activity.fixed_price}}</p>
                      <div class="count">
                        <QuantityControll :goodQuantity="food"/>
                      </div>
                  </div>
                </div>                  
                </li>
              </ul>
            </div>
          </li>
        </ul>
      </div> 
   </div>
  </div>
</template>
<script>
import Bscroll from 'better-scroll'
import QuantityControll from '../../components/shops/goodsQuantityControll'
export default {
  name:'order',
  data(){
    return {
      shopDetails:null,
      foodListScroll:null
    }
  },
  components: {
    QuantityControll
  },
  created(){
    this.getDetailsData()
  },
  methods:{
    getDetailsData(){
      this.$axios('/api/profile/batch_shop').then(res=>{
        // console.log(res.data.menu);
        // 为items每一个的元素增加一个count的属性 
        res.data.recommend[0].items.forEach(item=>{
          item.count = 0
        })
        //为menu下的food下加上一个count
        res.data.menu.forEach(item =>{
          item.foods.forEach(food =>{
            food.count = 0
          })
        })
        this.shopDetails = res.data
          
        this.$nextTick(()=>{
          this.ScrollInit();
        })
      })
    },
    ScrollInit(){
      //设置之后 ref为goodlist的div 只能用指针拖动 滚轮失效 前提是将该div 设置为 overflow: hidden
      this.foodListScroll=new Bscroll (this.$refs.goodlist,{
        click:true
      })
    },
    selectMenu(index){
      // console.log(index)
      console.log(this.$refs.category_title[index])
      let el = this.$refs.category_title[index]
      // console.log(this.$refs.category_title)
      this.foodListScroll.scrollToElement(el,250)
    }
  }
}
</script>
 
```



Vue.nectTick() 是在下次DOM更新循环结束之后执行延迟回调，在修改数据之后使用$nextTick，则可以在回调中获取更新后的DOM（dom的改变是发生在nextTick()之后），这个方法作用是当数据被修改后使用这个方法，会回调获取更新后的dom再render出来

　　Vue.nextTick()作用：在下次dom更新循环结束之后，执行延迟回调。在修改数据之后立即使用这个方法，获得更新后的dom
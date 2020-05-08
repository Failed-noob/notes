### vue 的生命周期

![](D:\QQ截图\life 周期钩子函数示意图.png)





通俗的讲: 就是一个Vue实例从创建到摧毁的历程 之间 所发生的事件 也称生命周期事件 ;





beforeCreate   由字面意思 就是创建前所执行的函数.   此事是无法访问data中的数据的;就是在 new一个Vue实例 执行此函数;



created 当实例完全创建时 此时可以访问data中的数据 和methods中的方法



beforeMount 当实例中的数据和方法 编译到浏览器中 但是没有真正渲染到页面上;



Mounted  实例创建的最后一个生命周期函数 当浏览器将实例中的data 渲染到页面上时 所执行的函数





看下面的例子吧

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script src="../vue.js/vue.min.js"></script>
</head>
<body>
    <div id="app">
        <p>{{msg}}---{{example}}---{{another}}</p>
        <input type="button" value="点我变更" @click='example=false'>
        <input type="text" v-model='another'>
    </div>
    <script>
        let Vm = new Vue({
            el:'#app',
            data:{
                msg:"hello",
                example:true,
                another:" "
            },
            beforeCreate() {
                console.log(this.msg) //此时msg没有创建到内存中 所以 此时无法获取到msg
            },
            created() {
                console.log(this.msg) //是上面一部的下一步 此时msg和methods中的方法和数据均可以访问
            },
            beforeMount() {//编译好 的模板  还未挂载到页面上的状态
                //我们通过DOM操作来获取到 上面P标签里面的元素;  
                //在vue中 尽量不推荐使用直接操作DOM 但是不是不能用DOM操作
                console.log(document.getElementById('app').children[0].innerHTML+'-----'+this.msg)
            },
            mounted() {
                //此时 编译好的 元素都完全挂载到页面中去了; 此时可以获取到 p标签中的 内容
                console.log(document.getElementById('app').children[0].innerHTML+'-----'+this.msg)

            },
            beforeUpdate() {
                // 这是当 元素更新前 
                console.log(document.getElementById('app').children[0].innerHTML+'{前面是变更前的状态}'+'-----'+this.another)
                console.log(document.getElementById('app').children[2])
            },
            updated() {
                console.log(document.getElementById('app').children[0].innerHTML+'{前面是更新后的状态}'+'-----'+this.example)

            },
        }) 
    </script>
</body>
</html>
```





效果如下:

![](D:\QQ截图\vue-lifeCircle.png)
### vue-2 





前面 先插一句:   js的setter 和 getter 先来看看MDN上的例子:

```javascript
//这是关于setter
var language = {
  set current(name) {
    this.log.push(name);
  },
  log: []
}

language.current = 'EN'; //这里我也可以直接调用函数 然后language.current('EN') 跟前面一样的结果 非要搞些看不懂的东西;
language.current = 'FA';

console.log(language.log);
// expected output: Array ["EN", "FA"]

//这是关于getter
var obj = {
  log: ['a', 'b', 'c'],
  get latest() {
    if (this.log.length == 0) {
      return undefined;
    }
    return this.log[this.log.length - 1];
  }
}

console.log(obj.latest);
// expected output: "c"

```

vue实例的 methods 属性 里面可以写方法  感觉说不清楚 上代码;

当方法再methods 中的时候 直接引用

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
    <div id="methods">
        <p @dblclick='disappear'>{{message}}</p>
    </div>
    <script>
        let Vm=new Vue({
            el:'#methods',
            data:{
                message: 'hello'
            },
            methods: {
               disappear:function(){
                   this.message=null;
               } 
            },
            // computed: {
            //     disappear:function(){
            //        this.message=null;
            //    }  
            // }
        })
    </script>
</body>
</html>
```



当方法在computed 计算属性中的时候 如下:  引用的时候 需要用括号调用  虽然不加括号 控制台不会报错 但加括号才会正常运行;



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
    <div id="methods">
        <p @dblclick='disappear()'>{{message}}</p>
    </div>
    <script>
        let Vm=new Vue({
            el:'#methods',
            data:{
                message: 'hello'
            },
            // methods: {
            //    disappear:function(){
            //        this.message=null;
            //    } 
            // },
            computed: {
                disappear:function(){
                   this.message=null;
               }  
            }
        })
    </script>
</body>
</html>
```



看看vue的监听属性 watch : (

**Vm.$watch(所需要监听的属性,function(变化后的属性值,变化前的属性值){**

**}**

)

上面的结论是从下面的代码中得来的;

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
        <p>现在数是:{{count}}</p>
        <button @click={{count++}}>+</button>
    </div>
    <script>   
    let Vm = new Vue({
        el: '#app',
        data:{
            count:1
        },
    })
       Vm.$watch('count',function(newer,old){
           console.log(old+'=>'+newer)
       }) 
    </script>
</body>
</html>
```





v-model  双向绑定; 先看代码



v-model 绑定的属性, 就下面这个例子而言, 在输入框中改变value值的时候,p标签中的message值 也会同步发生变化;

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
        <p>{{message}}</p>
       <input type="text" v-model='message'>
    </div>
    <script>
        let  Vm= new Vue({
            el:'#app',
            data:{
                message:'dfdasf'
            }
        })
    </script>
</body>
</html>
```





#### v-on 的事件绑定修饰符

![](D:\QQ截图\事件修饰符.png)



```html
<a href='https:://www.baidu.com' @click.prevent='tan'> 
//这样点击a标签也不会跳转 阻止默认行为
//这里解释以下.self  就是点击拥有这个修饰符的元素时才做出应答
//.capture  就是让以 捕捉的形式 进行下去
```


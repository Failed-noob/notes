### vue-filter 过滤器 / 键盘修饰符 / 自定义指令 (例如v-bind 之类的)



含义:
​	Vue.js允许自定义过滤器，可被用于一些常见的文本格式化。过滤器可以用在两个地方：双花括号插值和v-bind表达式。过滤器应该被添加在JavaScript表达式的尾部，由“管道”符号指示：



过滤器分为 局部过滤器和全局过滤器;



局部过滤器:

```html
<script>
// 创建 Vue 实例，得到 ViewModel
            var vm = new Vue({
                el: '#app',
                data: {
                    msg: '曾经，我也是一个单纯的少年，单纯的我，傻傻的问，谁是世界上最单纯的男人'
                },
                methods: {},
                //定义私用局部过滤器。只能在当前 vue 对象中使用
                filters: {
                    dataFormat(msg) {
                        return msg+'xxxxx';
                    }
                }
            });
    </script>
```



下面定义的时 全局过滤器;

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
        <p>{{previous | after('future')}}</p>
    </div>
    <script>
        //定义全局过滤器 第一个参数是固定的传入需要改变的参数 当然也可以传入多个参数;
        Vue.filter('after',function(previous,arg){
            return previous.replace('以前',arg)
        })
        let Vm = new Vue({
            el:'#app',
            data:{
                previous: '以前'
            }
        })
    </script>
</body>
</html>
```





对于绑定属性然后加一个过滤器 这一点 不知道是否有错误;



```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script src="../vue.js/vue.min.js"></script>
    <style>
        .clr {
            color: pink;
        }
    </style>
</head>
<body>
    <div id="app">
        <p>{{previous | after('future','--diffcult')|Part}}</p>
        <p :class="clr | Opsite">hello world</p>
    </div>
    <script>
        //过滤器可以串联,也可传递多个参数
        //定义全局过滤器 第一个参数是固定的传入需要改变的参数 当然也可以传入多个参数;
        Vue.filter('after',function(previous,arg,arg2){
            return previous.replace('以前',arg+arg2)
        })
        let Vm = new Vue({
            el:'#app',
            data:{
                previous: '以前',
                clr:true
            },
            //定义一个局部过滤器;
            filters:{
                Part(previous){
                    return previous+'---hello';
                },
                Opsite(clr){
                    return !clr;
                }
            }
        })
    </script>
</body>
</html>
```







#### 这是Vue 2.0 版本的定义键盘修饰符

全局按键修饰符:

比如 需要按下回车键之后文件提交 此时Vue 提供了  @keyup.enter='方法'

每个键盘对应着相应的键盘码 即 keyCodes   Vue专门为常用的几个键盘起了别名;



```html
            <input type="text" class="form-control" placeholder="请输入你的价格" v-model='price' @keyup.enter='add'>

//为相应的键盘码起别名
Vue.config.keyCodes.f2=113  此时113 所对应的键盘就是F2

```



**自定义指令(全局 ):** // 若为局部自定义指令 就跟filter | filters 之间差不多 片面上的区别 就是当 

Vue.directive(arg, { })  这时全局 

 directives:{

​					

​	}

**这为 局部**

 	在设置自定义指令时 前面必须要有 **v-** 的标志 只是约定俗成的 (在调用时 不需要加上v-前缀 但是在调用此命令时 需加上 **v-的**前缀);



Vue.directive ( ) 可以定义指令 第一个参数时 自定义指令的名称  第二个参数是一个对象,在对象中有一些指令相关的函数;



- **在每个函数中，第一个参数，永远是 el ，表示被绑定了指令的那个元素，这个 el 参数，是一个原生的JS对象**
- **`bind`: 每当指令绑定到元素上的时候，会立即执行这个 bind 函数，只执行一次，样式相关的可以在`bind`中设置**
- **`inserted`: 元素插入到DOM中的时候，会执行 inserted 函数【触发1次】，和JS行为有关的操作，最好在 inserted 中去执行，放置 JS行为不生效**
- **`updated`: 当VNode更新的时候，会执行 updated， 可能会触发多次**



#### 

![](D:\QQ截图\钩子函数初始.png)



在给元素设定样式是 用bind 函数   不管元素渲染是否成功  都是在指定的元素出现一个内联样式;

与 **JS** 行为有关的 的  用   inserted 函数   当元素完全渲染到页面上时 触发事件;





#### **钩子函数参数**

指令钩子函数会被传入以下参数：

- `el`：指令所绑定的元素，可以用来直接操作 DOM 。

- ```
  binding
  ```

  ：一个对象，包含以下属性：

  - `name`：指令名，不包括 `v-` 前缀。
  - `value`：指令的绑定值，例如：`v-my-directive="1 + 1"` 中，绑定值为 `2`。
  - `oldValue`：指令绑定的前一个值，仅在 `update` 和 `componentUpdated` 钩子中可用。无论值是否改变都可用。
  - `expression`：字符串形式的指令表达式。例如 `v-my-directive="1 + 1"` 中，表达式为 `"1 + 1"`。
  - `arg`：传给指令的参数，可选。例如 `v-my-directive:foo` 中，参数为 `"foo"`。
  - `modifiers`：一个包含修饰符的对象。例如：`v-my-directive.foo.bar` 中，修饰符对象为 `{ foo: true, bar: true }`。

- `vnode`：Vue 编译生成的虚拟节点。移步 [VNode API](https://cn.vuejs.org/v2/api/#VNode-%E6%8E%A5%E5%8F%A3) 来了解更多详情。

- `oldVnode`：上一个虚拟节点，仅在 `update` 和 `componentUpdated` 钩子中可用。

除了 `el` 之外，其它参数都应该是只读的，切勿进行修改。如果需要在钩子之间共享数据，建议通过元素的 [`dataset`](https://developer.mozilla.org/zh-CN/docs/Web/API/HTMLElement/dataset) 来进行。





#### 下面时自定义指令的全局定义和局部定义的简写方式;

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
        <p v-color='"50px"' v-Weight="'bolder'">{{msg}}</p> 
        <!--在给自定义指令传递参数时, 若为字符串则需要用单引号筐住 若只有单引号或者双引号则渲染不出来-->
    </div>
    <script>
        //定义一个全局指令
        Vue.directive('color',{
            bind:function(el,binding){
                el.style.color='pink';
                // console.log(binding)
            },
            inserted:function(el,binding){
               el.style.fontSize=binding.value;
                console.log(binding)
            },
            
            
        })
        let Vm=new Vue({
            el:'#app',
            data:{
                msg:'bigger than bigger'
            },
            directives:{
                Weight:function(el,binding){
                    el.style.fontWeight=binding.value;
                }
            }
            
        })
    </script>

</body>
</html>
```


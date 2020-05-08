### **Object 对象中的set & get**



首先setter & getter 这两设置的伪属性都可以通过delete删除 例如下面的第一个例子 delete lang.current 就可以删除了;

**先来说set**  set语法将 **对象属性** 绑定到要调用的函数;

```javascript
 let lang = {
      log:[],
      set current(name){
        this.log.push(name)
      }
    }
    console.log(lang.__proto__)
    console.log(lang)
    //伪属性
    lang.current = [1,23,234,3,232,2,2,2];
    console.log(lang.log)
```

set current 就是为对象定义一**个伪属性** 当改变这个值时,对象的setter将被执行  所以赋值的时候需要  language.current = 'ok"  同时调用setter 再language.log这个空数组里加上  赋值给lannguage .current 这个伪属性

再来看几个例子: 

```javascript
<script>
    //set 将对象属性绑定到要调用的函数
    let lang = {
      log:[],
      set current(name){
        this.log.push(name)
      }
    }
    console.log(lang.__proto__)
    console.log(lang)
    //伪属性
    lang.current = [1,23,234,3,232,2,2,2];
    console.log(lang.log)
    console.log('--------')
    //通过defineProperty 为当前对象定义setter
    let o = {
      a: 6
    }
    console.log('a之前的值',o.a)
    Object.defineProperty(o,'b',{set : function(x){
      this.a = x / 2 
    }})
    //跟上面的步骤差不多 给伪属性赋值
    o.b = 20 
    //此时 根据setter中的语句 对象中的a属性就发生了变化
    console.log('给伪属性赋值后a的值',o.a)

    console.log('---------')
     let expr = 'foo';

     let obj = {
       baz: 'bar',
     }
     Object.defineProperty(obj,[expr],{set : function(x){
       this.baz = x
     }})
     obj[expr] = 'hahahah'
     console.log(obj.baz)
  </script>
```



**get **

```javascript
console.log('\n','---------getter--------')

     let bar = {
       name:'donghan',
       get haha(){
         return this.name
       }
     }
     console.log(bar.haha)
     //用defineProperty  设置get
     let say='speak';

     let person = {
       age: 22
     }
     Object.defineProperty(person,[say],{get : function(){
       return this.age +10 
     }})
    console.log(person[say])
```



//set&get 

```javascript
 let unity = {
      a:1,
      b:'hello',
      set c(x){
        c = x
      },
      get c(){
        return c
      }
    }
    unity.c = 3
    console.log(unity.c) // 相当于创建了一个属性c
```


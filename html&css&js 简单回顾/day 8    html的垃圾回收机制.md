#### day 8    html的垃圾回收机制&     this的指向(重点)



​	**当一个对象 没有任何一个变量或者属性 对其进行引用时  此时该对象就是垃圾  由于垃圾过多 会导致程序的运行的过慢 甚至崩溃  所以 js会有一个自动的垃圾回收机制 所以我们不需要 也不能对垃圾回收进行操作;**

![](D:\QQ截图\垃圾回收.jpg)



![](D:\QQ截图\lajihuishou-2.png)





##### this的指向:



![](D:\QQ截图\this的指向.png)



```javascript
var name= 'haha';
function la() {
    alert(this.name);
}
la()  //haha this指向window 

var obj= {
    name: 'donghan',
    age: 22,
    gender: male,
    say: console.log(`我叫${this.name}`)
}
obj.say();// 我叫donghan        此时this指向 obj
```


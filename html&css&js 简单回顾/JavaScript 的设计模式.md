### **JavaScript 的设计模式**



学习设计模式，有助于写出可复用和可维护性高的程序

设计模式的原则是“找出 程序中变化的地方，并将变化封装起来”，它的关键是意图，而不是结构。



构造器模式:

```JavaScript
 /*构造函数*/
    function anestor(name,age){
      this.name =name;
      this.age =age;
       console.log(this)
    }
//在anestor 原型链上增加一个方法 然后用new 来 算是继承吧
	anestor.prototype.getInfo= function(){
      console.log(this.name+this.age)
    }
    let a= new anestor('DH',13) //当 new anestor后 this的指向anestor 这个函数对象 未new 之之前 this指向window
    console.log(a.name) //DH 
	console.log(a.getInfo())


 /*模块化模式*/
    /*每一个函数都会创建一个闭包[说白了 就是函数作用域] 当函数被创建，就会在时函数生成生成闭包。
      自执行函数 使用闭包时最好用 (function(){})() 
      (function(){})()   +function(){}()   ~function(){}()  -function(){}() !function(){}()
    */
    let example = (function(){
      // console.log('ojk')
      var a;
      return {
        a:1
      }
    })()
    console.log(example) //此时就将 函数内部变量 暴露出来了

//再来一个例子
var testModule = (function () {

  var counter = 0;

  return {

    incrementCounter: function () {
      return counter++;
    },

    resetCounter: function () {
      console.log( "counter value prior to reset: " + counter );
      counter = 0;
    }
  };

})();

// Usage:

//由于这是个自执行函数 所以这个匿名函数就是 return这个对象 控制打印testModel 就是一个对象
// Increment our counter
testModule.incrementCounter();

// Check the counter value and reset
// Outputs: 1
testModule.resetCounter();


//暴露模块模式 跟上面的 模块化模式很相似 都是返回对象
var myRevealingModule = function () {

        var privateCounter = 0;

        function privateFunction() {
            privateCounter++;
        }

        function publicFunction() {
            publicIncrement();
        }

        function publicIncrement() {
            privateFunction();
        }

        function publicGetCount(){
          return privateCounter;
        }

        // Reveal public pointers to
        // private functions and properties       

       return {
            start: publicFunction,
            increment: publicIncrement,
            count: publicGetCount
        };

    }();

myRevealingModule.start();
```


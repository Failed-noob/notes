### generator **函数**

```markdown
语法:  function * test(){
    /**/
}
```

在函数的声明的时候在函数名与function之间 加一个 ***; 还有 yield [产出] 关键字 只能用在 generator函数中,否则报错;** 当然 generator函数中不是必须需要 yield 的 但是它仍然会延迟进行 也同样需要用next() 方法来进行下一步的调用 毕竟 generator函数时返回一个 带有iterator接口的对象嘛!



generator 函数返回的是一个 有iterator 接口的对象  需要用 next() 方法才能访问到内部的 value值

**用next()方法的时候有一个前提, 将有函数名称 generator函数 赋值给 一个变量  例如 let a = rest() 不能用new关键字**

Generator 函数返回的遍历器对象，只有调用`next`方法才会遍历下一个内部状态，所以其实提供了一种可以暂停执行的函数。`yield`表达式就是暂停标志。

```javascript
//当 yield 在赋值表达式右边的时候, 需要用 ()包起来 或者放在另一个表达式中时 也需要如此

function* foo(x){
  let y = 2* (yield x); 
}

//next()的参数

function* f() {
  //下面为一个无限的for循环 在这个函数中 reset 永远不可能变为 -1;
  for(var i = 0; true; i++) {
    var reset = yield i;
    if(reset) { i = -1; }
  }
}

var g = f();
console.log(g.next())
console.log(g.next())
console.log(g.next())
console.log(g.next())
//当给next()一个true的参数的时候 reset会变为 true 然后循环会重置
console.log(g.next(true))
console.log(g.next())


console.log('--------')


function* foo1(x) {
  
  var y = 2 * (yield (x + 1));
  var z = yield (y / 3);
  return y+x+z;
}
let b = foo1(5)
console.log(b.next()) //yield (5+1)  value =6
console.log(b.next(6)) // { value: 4, done: false }  将yield(x+1) 设为 6  y=  2*6=12  => yield (12 /3 )  value => 4
console.log(b.next(3)) // { value: 20, done: true } 将yield(y / 3) 设为 3  => z=3  return x=5 y=12 z=3  5+12+3=20 value=>20

```



由于`next`方法的参数表示上一个`yield`表达式的返回值，所以在第一次使用`next`方法时，传递参数是无效的。V8 引擎直接忽略第一次使用`next`方法时的参数，只有从第二次使用`next`方法开始，参数才是有效的。



**Generator.prototype.return()**

可以返回给定的值,并中介遍历的Generator函数;

```javascript
function* gen() {
  yield 1;
  yield 2;
  yield 3;
}

var g = gen();

g.next()        // { value: 1, done: false }
g.return('foo') // { value: "foo", done: true }
g.next()        // { value: undefined, done: true }


//当执行return (7) 后 不执行try中的的代码 执行finally中的代码 最后执行 return 中的value
function* numbers () {
  yield 1;
  try {
    yield 2;
    yield 3;
  } finally {
    yield 4;
    yield 5;
  }
  yield 6;
}
var g = numbers();
g.next() // { value: 1, done: false }
g.next() // { value: 2, done: false }
g.return(7) // { value: 4, done: false }
g.next() // { value: 5, done: false }
g.next() // { value: 7, done: true }
```



yield * 表达式:

generator函数返回的是一个带有iterator接口的对象 所有它也可以用for-of 来遍历循环; 若在其他函数内部 需要遍历时 特别是很多函数嵌套 有些麻烦 这时就可以用yield * 



```javascript
function* foo() {
  yield 'a';
  yield 'b';
}
for(v of foo2()){
  console.log(v) 
} // output: a,b

function* bar() {
  yield 'x';
  yield* foo2();
  yield 'y';
}
for(v of bar()){
  console.log(v) 
}  //output: x,a,b,y
```







**作为对象属性的** **Generator函数**

```javascript
//简写
let obj = {
  * myGeneratorMethod() {
    ···
  }
};

let obj = {
  myGeneratorMethod: function* () {
    // ···
  }
};
```




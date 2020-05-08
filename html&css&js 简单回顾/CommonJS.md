AMD CMD COMMONJS



### CommonJS

　　CommonJS 是以在浏览器环境之外构建 javaScript 生态系统为目标而产生的写一套规范，主要是为了解决 javaScript 的作用域问题而定义的模块形式，可以使每个模块它自身的命名空间中执行，该规范的主要内容是，模块必须通过 module.exports 导出对外的变量或者接口，通过 require() 来导入其他模块的输出到当前模块的作用域中；目前在服务器和桌面环境中，node.js 遵循的是 CommonJS 的规范；

　　CommonJS 对模块的加载时同步的；

 

### AMD

　　AMD 主要是为前端 js 的表现指定的一套规范；而 CommonJS 是主要为了 js 在后端的表现制定的，它不适合前端；

　　AMD 是 Asynchronous Module Definition 的缩写，意思是 异步模块定义；采用的是异步的方式进行模块的加载，在加载模块的时候不影响后边语句的运行；

　　AMD 也是采用 require() 语句加载模块的，但是不同于 CommonJS ，它有两个参数；require(['模块的名字']，callBack)；requireJs 遵循的就是 AMD 规范；

 

### CMD

　　CMD 是 Common Module Definition 的缩写，是 seajs 推荐的一套规范，CMD 也是通过异步的方式进行模块的加载的，不同于 AMD 的是，CMD 的加载是按照就近规则进行的，AMD 依赖的是前置；CMD 在加载的使用的时候会把模块变为字符串解析一遍才知道依赖了哪个模块；

 

　　CommonJS 其实也有浏览器端的实现，原理是先将所有模块都定义好并通过 id 索引方便的在浏览器环境中进行解析；

　　AMD 的实现其实是通过 define 函数定义在闭包中，例如：define(id?: String，dependencies?: String[]，factory: Function | Object)；

　　　　其中，id 是模块的名字，是一个可选的参数；dependencied 指定了所要依赖的模块列表，是一个数组，每个依赖的模块的输出将作为参数一次传入 factory 中；如果没有指定 dependencies 的话，那么默认的就是 ["require"，"exports"，"module"]；factory 包括了模块的具体实现，它是一个函数或者对象；如果是函数，那么它的返回值就是模块的输出接口或者值；
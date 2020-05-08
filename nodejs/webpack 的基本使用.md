### webpack 的基本使用

*webpack* 是一个现代 JavaScript 应用程序的*静态模块打包器(module bundler)*。

- 入口(entry)
- 输出(output)
- loader
- 插件(plugins)



//vue.config.js 的基本配置

```javascript
// webpack 的基本配置
let path = require('path');

module.exports= {
  //入口
  entry:'./src/index.js',
  output: {
    filename:"bundle.js", //打包后的文件名
    path:path.resolve(__dirname,'build')
  },
  mode:"development"  //default 为 production
}
```





```json
//package.json  

{
  "devDependencies": {
    "webpack": "^4.43.0",
    "webpack-cli": "^3.3.11"
  },
  "scripts": {
    "build": "webpack --config webpack.config.js"
  }
}

```



这个script属性 里面的 的     可以在控制台命令行工具通过  cnpm /npm run build

来运行打包; 或者直接 webpack 或者 npx webpack



使用 webpack-dev-server 可以搭建一个服务器，然后服务器上运行打包后的 代码

下面的是在package.json中 对于webpack-dev-server 的运行

```json

```



使用npm run dev / npx webapck-dev-server 即可运行 webpack-dev-server 

```JavaScript
devServer:{
    // 这是 对webpack-dev-server 的配置 首先肯定要安装 webpack-dev-server
    port: 3000, //改变端口号，
    progress:true,
    contentBase:'./build' //相当于node中设置 静态服务的地址

  },
```

由于我打包的是一个 js文件 所以需要创建一个 html 来引入js文件才能显示; 但是一般不可能在打包的文件夹再创建一个html 

此时就要用的插件了; 毋庸置疑 插件使用之前都是要安装的;



```JavaScript
// webpack 的基本配置
let path = require('path');
//插件引入
let HtmlWebpackPlugin = require ('html-webpack-plugin')

module.exports= {
  devServer:{
    // 这是 对webpack-dev-server 的配置 首先肯定要安装 webpack-dev-server
    port: 3000, //改变端口号，
    progress:true,
    contentBase:'./build' //相当于node中设置 静态服务的地址

  },
  //入口
  entry:'./src/index.js',
  output: {
    filename:"bundle.js", //打包后的文件名
    path:path.resolve(__dirname,'build')
  },
  mode:"development",  //default 为 production
  plugins:[
    // plugins 为一个数组, 所有的引入的插件都在这配置
    new HtmlWebpackPlugin({
      // 配置插件
      template:'./src/index.html', //配置打包过去html 以这个html为模板
      filename:'index.html' //编译之后 这个玩意没有打包
    })
  ]
}
```

先运行 cnpm run  build 进行打包 然后运行 cnpm run dev 运行 webpack-dev-server  运行之后就可以显示了



### **loader** 

```javascript
 module: {
    rules: [
      {
        test: /\.css$/,
        use: [
          { loader: 'style-loader' },
          {
            loader: 'css-loader',
            options: {
              modules: true
            }
          }
        ]
      }
    ]
  }
```


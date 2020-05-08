### node的express 框架

express基于 Node.js 平台，快速、开放、极简的 Web 开发框架



安装 : 

npm/cnpm install express --save;



然后一个简单的例子:

```javascript
let express =require('express');
let app = express();
// console.log(app)
app.get('/',function(req,res){
  res.write('dsfdsf')
  res.end()
})
app.listen(80,function(){
  console.log('Server is running at: ','http://127.0.0.1')
})
```





跟vue有vue@cli 一样  node的express 也有相应的快速搭建工具 express-generator

全局安装之后 到一个空文件夹中 cmd  

express -e project_name

或者 express -e        [ -e 添加ejs 模板引擎的支持  默认是jade 模板]

![](D:\QQ截图\express框架目录.PNG)



bin  可执行文件目录 这里面有监听的端口号

node_modules 依赖包的目录

public 所有静态文件的根目录 [在app.js中通过中间件 static 设置 静态文件的资源的目录]  __dirname表示 app.js所在位置

**app.use(express.static(path.join(__dirname, 'public')));**

routes 路由模块目录 动态文件的目录 [也需要在app.js中引入]

views 视图目录 用于存储模板 [在app.js 中设置]

**// view engine setup**

**app.set('views', path.join(__dirname, 'views'));**

**app.set('view engine', 'ejs');**



app.js 主文件 

package.json  项目信息 依赖包的版本信息



### **路由的说明**






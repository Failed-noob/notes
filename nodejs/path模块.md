### **path模块**



首先引入嘛!

常用的方法: 

```JavaScript
//path.basename() 方法返回 path 的最后一部分

path.basename('/foo/bar/baz/asdf/quux.html');
// 返回: 'quux.html'

//path.dirname(path) 方法返回 path 的目录名

path.dirname('/foo/bar/baz/asdf/quux');
// 返回: '/foo/bar/baz/asdf'

//path.extname(path) 方法返回 path 的扩展名，从最后一次出现 .（句点）字符到 path 最后一部分的字符串结束

path.extname('index.coffee.md');
// 返回: '.md'

//path.parse(path) path.parse() 方法返回一个对象，其属性表示 path 的重要元素。这个方法就是上面三个方法的综合

path.parse('/home/user/dir/file.txt');
// 返回:
// { root: '/',
//   dir: '/home/user/dir',
//   base: 'file.txt',
//   ext: '.txt',
//   name: 'file' }

//path.join(path) 方法使用平台特定的分隔符作为定界符将所有给定的 path 片段连接在一起，然后规范化生成的路径。只是保证路径的规范化 有可能这个地址找不到相应的文件
path.join('/foo', 'bar', 'baz/asdf');
// 返回: '/foo/bar/baz/asdf'
```


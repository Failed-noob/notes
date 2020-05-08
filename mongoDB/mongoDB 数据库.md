### mongoDB 数据库 基本操作



定义:  mongoDB 数据库 是非关系性数据库 (NOsql) 基于分布式文件存储的开源数据库系统; 数据结构 由 键值对组成  (key => value )  类似于ＪＳＯＮ对象；



**主要特点：**

- ＭｏｎｇｏＤＢ　是一个　面向文档存储的数据库　操作起来比较简单；
- 可以在ＭｏｎｇｏＤＢ记录中设置任何索引　来实现更快的排序；
- 若负载增加　它可以分布在计算机网络中的其他节点上　即　分片；
- ＭｏｎｇｏＤＢ　支持丰富的查询表达式　查询指令使用JSON形式的标记　可轻易查询文档内嵌的对象及数组；
- ＭｏｎｇｏＤＢ　使用ｕｐｄａｔｅ（）　命令　可以实现替换文城的文档　或者　一些指定的数据字段；
- ＭｏｎｇｏＤＢ　中的Ｍａｐ／　ｒｅｄｕｃｅ　主要用来　对数据进行批量处理和聚合操作；
- Map和Reduce。Map函数调用emit(key,value)遍历集合中所有的记录，将key与value传给Reduce函数进行处理。
- Map函数和Reduce函数是使用Javascript编写的，并可以通过db.runCommand或mapreduce命令来执行MapReduce操作。
- GridFS是MongoDB中的一个内置功能，可以用于存放大量小文件。
- MongoDB允许在服务端执行脚本，可以用Javascript编写某个函数，直接在服务端执行，也可以把函数的定义存储在服务端，下次直接调用即可。
- MongoDB支持各种编程语言:RUBY，PYTHON，JAVA，C++，PHP，C#等多种语言。



首先如何运行 MongoDB的可视化工具 robot 3t   

```markdown
先打开cmd 命令;
然后在安装mongoDB的bin文件下运行   mongod --dbpath e:\data\db  ( 此时 好像就已经把打开 了 但是还是按照官网上的操作 如下)

同样 跟上面一样 在bin文件下 运行 mongo.exe  (当然这句命令行需要重新打开一个窗口命令行)
```



在　ＭｏｎｇｏＤＢ　的可视化工具　　Robot　３Ｔ　中　可进行如下操作

```markdown
／／　　创建数据库　
ｕｓｅ　数据库名
// 若你想再创建一个数据库 你需要 use 数据库名 后 再db到新创建的数据库中 然后插入一些数据后 然后才成功 否则 就会在上一个数据库的下 创建另一个集合

//删除数据库
db.dropDatabase()

／／　显示　所有的数据库
ｓｈｏｗ　ｄｂｓ　

//显示所有集合
show collections

//创建集合 collection
db.createCollection(name, options) options 是可选的 

//删除集合
db.collection.drop()   [ collection 是集合名  是drop  而不是remove  注意哦]

//更新文档 用于已存在的文档
db.collection.update(
   <query>,
   <update>,
   {
     upsert: <boolean>,
     multi: <boolean>,
     writeConcern: <document>
   }
)
[其中的 upsert ]

query : update的查询条件，类似sql update查询内where后面的。
update : update的对象和一些更新的操作符（如$,$inc...）等，也可以理解为sql update查询内set后面的
upsert : 可选，这个参数的意思是，如果不存在update的记录，是否插入objNew,true为插入，默认是false，不插入。
multi : 可选，mongodb 默认是false,只更新找到的第一条记录，如果这个参数为true,就把按条件查出来多条记录全部更新。
writeConcern :可选，抛出异常的级别。

data={
    title: 'MongoDB 教程', 
    description: 'MongoDB 是一个 Nosql 数据库',
    by: '菜鸟教程',
    url: 'http://www.runoob.com',
    tags: ['mongodb', 'database', 'NoSQL'],
    likes: 100
}
db.Testthree.insert(data)
db.Testthree.update({"title":"MongoDB 教程"},{$set:{'title':'MongoDB'}})

//删除文档 
db.collection.remove(
   <query>,
   <justOne>
)  [justOne 若设置 true / 1 就只会删除 对应的一条    默认是false 就会删除匹配的全部数据]
db.col.remove({'title':'MongoDB 教程'})  [这是数据中的一条 但是当执行后 数据会全部消失]


//查询文档

db.collection.find(query, projection)
第二条是可选的

```


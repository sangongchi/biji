### MongoDB 的连接使用

---

#### 1. node 连接 MongoDB 

- Mongoose 是mongoDB的一个对象模型库,封装了mongoDB对文档的一些增删改查等常用方法,让nodejs操作mongoDB数据库变得更容易
- 安装  mongoose  `npm i --save mongoose`
- 在项目中共创建**db**文件夹专门存放数据相关的文件

```js
//connect.js
const mongoClient=require('mongoose')

let url = "mongodb://127.0.0.1:27017/testLogin";
/*
 * 有密码的连接方式
 * 数据库名 test
 * 用户名 admin
 * 密码  123456
 * */
// mongoose.connect('mongodb://admin:123456@localhost:27017/test');
//连接数据库
mongoClient.connect(url,{useNewUrlParser:true,useCreateIndex:true,useUnifiedTopology:true})

const db=mongoClient.connection;      //数据库的连接对象
db.on('error',(err)=>{
  throw "数据库连接失败"+err
})
db.once('open',()=>{
  console.log("数据库连接成功")
})
```

- **model**文件夹 用来存放不同类型的Model

    - **Model**
        由Schema构造生成的模型,具有抽象属性和行为的数据库操作

        `var PersonModel=db.model('person',PersonSchema)`

    - **Schema**
        是一种文件形式存储的数据库模型骨架,不具备数据库的操作能力,即定义数据类型

```js
// 用户登录注册版块  userModel.js

const mongoClient=require('mongoose')
//建立用户表
const UserSchema=new mongoClient.Schema({
    username:{
        type:String,   //指定类型
        unique:true,   //值唯一
        trim:true,     //去掉两边空格  
        require:true   //必填项
    },
    password:{
        type:String,
        index:true,     //创建索引 或者使用 unique
        maxlength:20, //只能用于string类型
        minlength:10
    },
    age:{
        type:Number, //min与max必须在Number中
        min:0,
        max:130
    }
})

//建立用户数据模型
const User = mongoClient.model('User',UserSchema)
//将数据模型抛出
module.exports={User}
```

#### 2.操作数据库

- 查询数据库数据

```js
//1.查询表中的所有数据信息  User为上边创建的  Model  可以对数据库进行增删改查的实例对象
// find() 可以返回匹配条件的所有数据。 如果未指定条件，find() 返回集合中的所有数据。
User.find({},(err,data)=>{
    if(err){
        console.log(err)
        return 
    }
    console.log(data)
})

//2.按条件查询一个数据
User.findOne({uaername:'sangongchi'},function(err,data){
    console.log(data)
})
//3. 按条件查询所有
User.find({sex:'男'},(err,data)=>{
    console.log(data)
})
```



```js
//常用的查询语句总结
User.find()  //查询所有记录 sql:select * from users

User.find(查询条件)
User.find({'age': 22}); //查询 age = 22 的记录  select * from users where age = 22;
User.find({age:{$gt:20}}) //查询年龄大于20的
User.find({age:{$lt:20}}) //查询年龄小于20的
User.find({age:{$gte:20}}) //查询年龄大于等于20的
User.find({age:{$1te:20}}) //查询年龄小于等于20的
User.find({'age': {$ne: 22}}); //查询 age != 22 的记录

User.find({'age': {$gte: 23, $lte: 26}}); //查询 age >= 23 并且 age <= 26
User.find({$or: [{age: {$gte: 23}}, {name: '张三'}]); //查询 age >= 23 或者 name == '张三'

User.find({'name': /mongo/}); //查询 name 中包含 mongo 的数据  select * from users where name like %mongo%;
User.find({'name': /^mongo/}); //查询 name 中已 mongo 开头的数据
User.find({'name': /mongo$/}); //查询 name 中已 mongo 结尾的数据

User.find({}, {name: 1, age: 1}); //查询 指定列 name 、age 的数据
User.find({age: {$gt: 25}}, {name: 1, age: 1}); //查询 指定列 name 、age 并且 age > 25

User.find().sort({age: 1}); //升序 倒序传-1

User.find({name:'zhangshan'},{age:20}) //查询 name = zhangsan , age = 20 的数据

User.find().limit(5); //查询 前5条数据
User.find().skip(10); //查询 10条以后的数据
User.find().limit(10).skip(5); //查询 在 5 - 10 之间的数据
User.find().count(); //查询 某个结果集的记录条数

User.findOne(); //查询第一条数据

//使用skip（） 和limit（） 实现分页
pageNum 当前第几页
pageSize 每页显示多少条
totalPage 一共有几页 Math.ceil (totalSize/pageSize)
totalSize 一共有多少条数据 db.XXX.find().count()

User.find().skip((pageNum - 1) * pageSize).limit(pageSize)  //第一页
User.find().skip(10).limit(10)                              //第二页
User.find().skip(20).limit(10)                              //第三页
```



- 增加数据

```js
//insertOne  插入一条
//insertMany 插入多条
User.insertOne({})

//5. 添加数据
var u = new User({
    name: 'cc',
    age: 20,
})
u.save((err) => {
    if (err) {
        console.log('添加失败');
        return;
    }
    console.log('添加成功');
})
```

- 删除和更新数据

```js
//6. 更新数据
User.updateOne(
    {'id': 'id值'},
    {name: 'sangongchi'},
    (error,data)=>{
        if(error){
            return console.log('update error');
        }
        console.log(data);
} )
//7. 删除数据
User.deleteOne({'id':'id值'},(error,data)=>{
    if(error){
        console.log('delete error');
        return;
    }
    console.log('删除成功',data);
})
```









##### 参考链接

- 原文链接：https://blog.csdn.net/qq_37674616/article/details/86680680


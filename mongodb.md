/*****04-14****************************/

 mysec 关系行数据库～～～～～～没有学过  
数据库分俩种: 关系数据库 ，非关系数据库  
关系型数据库 如同一张表一样。SQL mysec(开源免费) noSQL(google)  
CSV :exce 可以导入CSV 以“|”等符号为间隔符 可以导入关系行书库库  
非关系数据库，如同一个人的个人资料。  
redus memcache  ->持久化(大公司增加的缓存机制，并不是数据库)  
mongodb  
官方网站:https://www.mongodb.com/  
中文文档:https://  
安装mongodb ubuntu  
      sudo apt-key dav --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6
nest  
service 启动你相关服务器相应的服务。  
远程mongodb服务器 mongodb//mydb:asdfgh@ds151137.mlab.com:51137/mydb  
robomongo.org  
sudo apt update 更新  
sudo apt upgrade 升级  
在etc/apt/source.list.d 输入命令$ echo "deb [ arch=amd64,arm64 ] http://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list  
  
重新加载本地包数据库  
sudo apt-get update  
安装mongoDB包  
sudo apt-get install -y mongodb-org  
  
Ctrl + a 移动到命令行头的位置  
sudo apt install openssh-server  
ssh name@dizhi  
  
dbPath:存储 /var/lib/mongodb  
sudo service mongod start 新建mongodb  
port:端口号 27017mongodb 的默认端口号  
     什么是端口号:  
  
     tftp:文件传输协议  
ps ax 查看运行程序  
mongo 进入mongo  
～更改玩mongo 的IP 后 (该前复制)  
sudo serbice mongod restart  
  
mongo 地址:27017 链接世界任意的服务器  
mongo  推出  
show dbs      
show collections  
use<db_name> 建立数据库  
db.foo.find() foo 的内容  
        switched to db stu  切换到db stu//不是代码  
db stu insert({"name":'Fenghao Lan','sex':'M','age':80})  
db.dropDatabase()删除数据库  
  
db.one.update ({'name':'ABC'},{$set:{'age':20}}) 建立数据（专业术语就是创建集合）  
  
wget https://download.robomongo.org/0.9.0/linux/robomongo-0.9.0-linux-x86_64-0786489.tar.gz  
进到这个目路下的./robomongo 里面  
robomongo-0.9.0-linux-x86_64-0786489/bin$  
/**使用robmongo**/  
  打开robmongo 文件夹 的bin文件 直接运行 robmongo  
/*******练习打字的软件 推荐**********************/
  
sudo apt-get install ktouch  下载ktouch  
sudo apt-get update --fix-missing  
sudo apt-get install ktouch  
ktouch 运行 ktouch  
  
  /***********04-17***********/  
  /***********link 远程使用 bootcdn.cn***************/  
  
www.mlab.com 注册一个  
帐号:Tuishui  
密码:yuanhui_123  
  
安装mongodb包  并初始化一个一个package.json 文件：  npm init --yes  
本地安装mongodb 包 并写入package.js文件中：  
  npm install mongodb --save-dev  
  npm i mongodb -d  
链接mongodb 数据库  
创建一个app.js  
var MongoClient = require("mongodb").MongoCLient;  
var assert = require('assert');  
var url = "mongodb://mydb:"mima@ds151137.mlab.com.51137/mydb;  
MongoClient.connect(url,function(err,db){  
  assert.equal(null,err);  
  console.log('connected coorectly toserver.');  
  db.close();  
  });  
  
  /**************插入文档************/  
bd.one.omsert({'name':'zhao4','age':12});  
线保存于变量中:  
doc = {'name':'zhangsan','age':13}; 创建  
db.one.insert(doc); 插入  
  
db.collectionName.insert(doc)  
db.collectionName.save(doc)  
  /*****************更新***********************/  
  db.collectionName.update()  
  db.collectionName.save()   
  
  db.collectionName.update(  
    {quety},  
    {update},  
    {  
      upsert:<boolean>,  
      multi:<boolean>,  
      writeConcern:<document>,  
    }  
    )  
    query:update 的查询条件  
    update:update对象和一些更新的操作符(如$,$inc)，也可以理解为sq1、update 查询内set后面的  
    upsert:可选，如果不存在update的记录，是否插入objNew，true为插入，默认false，不插入。  
    multi:可选，mongodb 默认是false，只更新找到的第一条记录，如果这个参数为true，就把按条件查出来的多条记录全部更新。  
    writeConcern:可选，抛出异常的级别  
    /**************更新条件，或者说是显示文件***************************/  
    //更新第一条符合条件  
    db.one.update({"name":"zhangsan"}, {$set:{"age": 30}})  
  
    //更新所有符合条件  
    db.one.update({"name":"zhangsan"}, {$set:{"age": 30}}, false,true)  

    //没有符合条件的,添加一条文档进去
    db.one.update({"name":"zhangsan"}, {$set:{"age": 30}}, true,true)

    //将所有name=zhangsan的文档的age增加5  
    db.one.update({"name":"zhangsan"}, {$inc:{"age": 5}}, false,true)

    //将所有name=zhangsan的文档的age和course字段删除   
    db.one.update({"name":"zhangsan"}, {$unset: {"age":1, "course":1}}, false,true)

    //在一个数组域中添加一个数据并且将size域的值加１
    db.one.update({"age":10}, {$push:{"course":"html"}, $inc:{"size": 1}}, false, false)

    //在一个数组域中添加多个数据
    db.one.update({"age":10}, {$pushAll:{"course":["html", "python"]}}, false, false)

    //删除数组域中的一个数据
    db.firstClass.update({"age":20},{$pop:{"course":-1}},false,false) //删除course第一个
    db.firstClass.update({"age":20},{$pop:{"course":1}},false,false) //删除course最后一个

    //删除数组域中的某个特定数据
    db.firstClass.update({"age":20}, {$pull: {"course": "python"}}, false,false)

    //删除数组域中的多个数据
    db.firstClass.update({"age":20}, {$pullAll: {"course": ["python", "c"]}}, false,false)

    //修改某个域的名字
    db.firstClass.update({"age":20}, {$rename: {"course": "class"}}, false,false)

    //在某个数组域中添加数据(数据不存在时，才会添加)
    db.firstClass.update({"age":20}, {$addToSet: {"course": "python"}}, false,true)

/*******查找****************/
**/
db.collectionName.find()
db.collectionName.findOne()
查找所有文档:
db.collectionName.find()
/**/
***按照条件操作符查找：***
db.collectionName.find({"age": {$lt: 10}})   //　查询年龄小于　10的文档  
db.collectionName.find({"age": {$lte: 10}})   //　查询年龄小于等于　10的文档  
db.collectionName.find({"age": {$gte: 10}})   //　查询年龄大于等于　10的文档  
db.collectionName.find({"age": {$gt: 10}})   //　查询年龄大于　10的文档  
db.collectionName.find({"age": {$ne: 10}})   //　查询年龄不等于　10的文档    
db.collectionName.find({"age": {$mod: [10,0]}})   //　查询年龄能被10整除文档  
db.collectionName.find({"age": {$not: {$mod: [10,0]}}})// 查询年龄不能被10整除的文档  
db.collectionName.find({"course": {$all: ["english", "math"]}})  //查询course包含english和math的文档  
db.firstClass.find({"course": {$size : 3}})  //查找　course数组元素个数等于３的文档  
***按照and条件查询：同时满足所有条件***  
db.collectionName.find({"name":"lisi", "age":10})  // 查找name="lisi", age=10的文档  
db.collectionName.find({"name":"lisi", "age":10}).pretty()  //按照合适的格式显示　  　
12  
***按照or条件查询：满足其中的一个条件即可***  
db.collectionName.find({$or: [{"age":10}, {"age": 11}]}).pretty() //查找age=10 or age=11的文档  
***and和or条件混合使用***  
//查找　name=lisi and (age=10 or age=11)的文档  
db.collectionName.find({"name":"lisi", $or:[{"age":10},{"age": 11}]}).pretty()  
/*****************************/  
控制查询到的文档的数量：limit()  
db.collectionName.find().limit(2) //输出查询的到的前两条文档  
  
跳过查询到的前几条文档,输出其他文档：skip()  
db.collectionName.find().skip(1) //跳过前１条文档，从后边开始显示  
  
统计查询到的文档个数：　count()  
db.collectionName.find().count()  
  
对查询结果进行排序：　　　　　　  
db.collectionName.find().sort({"age": 1}) //按照age值进行升序排列  
db.collectionName.find().sort({"age": -1}) //按照age值进行降序排列  
  
将查询到的文档按照指定的域输出：　　　  
db.collectionName.find({}, {"name": 1, "age": 1}) //查询到的文档，仅仅输出name和age两个域  
/*************删除数据******************/  
db.collectionName.remove()  
  
/**MongoDB索引**/
  
 索引视为了提高查询效率，适用索引可以快速访问数据库表中的特定信息/索引是对值进行排序的一种结构  
 如果没有索引那么查找时会扫描整个集合，数据量大时效率会很低:  
  
 //1升序索引，　-1 降序索引  
db.collectionName.ensureIndex({key: 1})  
db.collectionName.ensureIndex({"age": -1, "name": 1})  
  
//创建唯一索引，name域不可以有重复的值  
db.collectionName.ensureIndex({"name": 1}, {"unique": true})  
  
//删除索引  
db.collectionName.dropIndex({"name":1})  
//删除所有索引  
db.collectionName.dropIndexes()  
  
/**MongoDB聚合**/  
aggregte主要用于文档数据的统计计算。  
db.collectionName.count()统计集合文档个数  
db.collectionName.count({'age':10})统计集合中符合条件的文档个数  
db.runCommand({"disinct":"collectionName"},{"key":"name"})显示集合中name值不一样的结果  
db.collectionName.aggregte();  
//按照name值分组，并计算每组的个数  
  
db.collectionName.aggregate([{$group:{_id:"$name", num:{$sum:1}}}])  
  
//按照name值分组，并计算每组中年龄的总和  
db.collectionName.aggregate([{$group:{_id:"$name", num:{$sum:"$age"}}}])  
  
//按照name值分组，并计算每组中年龄的平均值  
db.collectionName.aggregate([{$group:{_id:"$name", num:{$avg:"$age"}}}])  
  
//按照name值分组，并计算每组中年龄的最小值  
db.collectionName.aggregate([{$group:{_id:"$name", num:{$min:"$age"}}}])  
  
//按照name值分组，并计算每组中年龄的最大值  
db.collectionName.aggregate([{$group:{_id:"$name", num:{$max:"$age"}}}])  
  
//按照name值分组，并计算每组中第一个年龄值  
db.collectionName.aggregate([{$group:{_id:"$name", num:{$first:"$age"}}}])  
  
//按照name值分组，并计算每组中最后一个年龄值  
db.collectionName.aggregate([{$group:{_id:"$name", num:{$last:"$age"}}}])  
  
/**MongoDB聚合管道**/
 MongoDB聚合管道用于在一个条件处理完毕之后将结果传递给下一个条件进行处理。  
 $project:用于修改文档结构。  
 $match:用于过滤数据，只输出符合条件的文档。  
 $limit:用来限制MongoDB聚合管道返回的文档数。  
 $sort:将输入文档排序后输。  
 db.collectionName.aggregate({$project:{name:1, age:1, newname:"$oldname"}}) //修改域名　　  
db.collectionName.aggregate({$project:{_id:0 ,name:1, age:1}}) //删除_id, 其他域不可删    
db.firstClass.aggregate([{$project:{name:1, age:1, course:1, test:{$add:["$age",10]}}}]) //添加新域  
db.collectionName.aggregate([{$match:{"age":10}}, {$limit:2}]) //显示输出2条　　  
db.collectionName.aggregate([{$match:{"age":10}}, {$sort: {"name": 1}}]) //输出按照name升序排列　        　   

/***********************************************/
/**远程服务器**/
/***********************************************/

使用远程的mongodb服务器
在www.lmab.com 网站注册帐号，可以免费创建0.5G的远程mongodb服务器
'mongodb://mydb:asdfgh@ds151137.mlab.com:51137/mydb'

链接mongodb数据库
```
var MongoClient = require('mongodb').MongoClient;
var assert = require('assert');

var url = 'mongodb://mydb:asdfgh@ds151137.mlab.com:51137/mydb';
MongoClient.connect(url, function(err, db) {
  assert.equal(null, err);
  console.log('Connected correctly to server.');
  db.close();  
});  
```
与本地操作不同的是，远程服务器操作是用代码操作的而其名字是用conllection('restaurants')写明
而且程序几乎都将加入一个返回函数，失败输出err 成功输出callback();  

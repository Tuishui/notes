/****04-19*************/
**Express**
什么是Express ?
   Express.js 是基于Node.js中的HTTP模块和Connect组建的WEB框架，这些组建叫做中间件，他们是以约定大于配置原则作为开发的基础理念
Express 安装
  npm i express-generator -g
  npm i express --save
  express -e demo

  /**路由器**/
  用来实现一个动态网页
  ~~~node.js
  var express =require('express');
  var app = express();

  app.get('/',(req,res)=>{
    res.send('Hello world!');
    })
  app.liseten(3000);
 ~~~

 启动脚本web.js的app.get方法，用于指定不同的访问路径所对应的回调函数，这就是"routing"路由。实际应用有多个路由器记录

**例如：**
~~~
module.exports = function(app){ //放在routes文件之中必须的.

var express = require('express');
var app = express();

app.get('/', function(req, res){
  res.send("Hello world!");
});

app.get('/doc', function(req, res){
  res.send('doc page');
});

app.get('/admin', function(req, res){
  res.send('admin page');
});
};
~~~


~~~
var express = require('express');
var app = express();
var routes = require ('./routes/routes.js')(app);
app.listen(3000);
~~~
var a = 正则表达式
app.get('a',function(req,res){
   res.send(a);
  });

##响应方法
下表中响应对象想(res)de 方法可以想客户机发送响应，并终止请求/响应循环。如果没有从路由器处理程序调用其中任何方法，客户机请求将保持挂起状态。
```
res.download() //提示将要下载文件。
res.end()   //结束响应进程
res.json()  // 发送JSON响应。
res.jsonp()  //在JSONP 的支持下发送JSON响应
res.redirect()  //重新向请求。
res.render()  //呈现视图模板。
res.send()  //发送各种类型的响应
res.sendFild  //以八位元流形式发送文件
res.sendStatus()  //设置响应状态码并以响应主体形式发送其字符串表示

```
##中间件
什么是中间件:中间件(middleware)就是处理HTTP请求的函数。它最大的特点就是，一个中间件处理完，再传递给下一个中间件。``实例在运行中，会调用一系列的中间件``

##模板引擎用于express
在Express 可以呈现模板文件之前，必须设置以下应用程序设置：
views:模板文件所在目录。
viw engine:要适用的模板引擎
npm install jade --save
npm install ejs --save


set方法用于指定变量的值
使用 set方法，为系统变量views和view engine 指定值
```
app.set('views' ,__dirname + '/views');
app.set('view engine','jade'); //指定模板后缀名为jade
```
##编写启动脚本
在项目目录中，建立文件一般命名为app.js
```
var express = require('express');
var app = express();
//设置 port 变量，为访问端口
app.set('port',process.env.PORT || 3000);
//设置views变量，意为视图存放的目录
app.set('views',path,join(__dirname,"views"));
//设置view engine 变量，意为网页模板引擎
app.set('view engine', 'jade');

app.use(express.favicon());
app.use(express.logger('dev'));
app.use(express.bodyParser());
app.use(express.methodOverride());
app.use(app.router);

// 设定静态文件目录，比如本地文件
// 目录为demo/public/images，访问
// 网址则显示为http://localhost:3000/images
app.use(express.static(path.join(__dirname, 'public')));
app.listen(app.get('port'));
```
以上代码生成express实例，赋予变量app。设定express示例的参数。上面代码中set方法用于设定捏不变量，use方法用于调用express的中间件。最后调用实例方法listen，让其监听事件先设定的端口(3000);

##配置路由
在项目目录之中，建立一个子目录view,用于存放网页模板。
```
var express = require('express');
var app = express();

app.get('/', function(req, res) {
   res.sendfile('./views/index.html');
});

app.get('/about', function(req, res) {
   res.sendfile('./views/about.html');
});

app.get('/article', function(req, res) {
   res.sendfile('./views/article.html');
});

app.listen(3000);
```
##安装模板引擎
Express支持多种模板引擎,这里采用EJS 模板引擎的服务器端版本ejs模板引擎。
安装模板引擎之后，就要改写app.js
```
var express = require('express');
var app = express();

app.set('view engine', 'ejs');
app.set('views', __dirname+'/views');


app.get('/', function (req, res){
	res.render('index', {name: 'express'});
});

app.get('/about', function(req, res) {
	res.render('about');
});

app.get('/article', function(req, res) {
	res.render('article');
});

app.listen(3000);
```
/**ejs模块引擎**/
注意到任何在<% %>之间的代码都被执行了，而在<%= %>标签内的都把自己返回的HTML 字符串插入到了当前位置里。我们需要添加
javascript代码来控制模板的载入的渲染。

##forEach的使用
如果一条数据，我们可以随意的传送，但是如果是多条数据怎么办？在这里EJS 提供了一个forEach来解决额一组数据的处理问题。
```
app.get('/about', function(req, res) {
  var info = [{name: 'Mary', age: 20},
  {name: 'Ben', age: 32},
  {name: 'Scotch', age: 21}
];
	res.render('about', {
    info: info,
    title: "Information"
  });
});
```
下面是html文件，这里面用到的就是forEach来处理一组数据的显示。
```
<div>
  <h2> <%= title %> </h2>
  <ul>
    <% info.forEach(function(info){ %>
      <div>
  		<li><b>name:</b><%= info.name %></li>
  		<li><b>age:</b><%= info.age %></li>
	</div>
    <% }); %>
  </ul>
</div>
```
##使用嵌套模板
index.ejs代码：
```
<div>
  <h2> <%= title %> </h2>
  <ul>
    <% info.forEach(function(info){ %>
      <%- incldue('item', {info: info})%>
    <% }); %>
  </ul>
</div>
```
将引入item.ejs模板文件显示
item.ejs
```
<div>
  <li><b>name:</b><%= info.name %></li>
  <li><b>age:</b><%= info.age %></li>
</div>
```
/**GET/POST获取数据**/
***GET使用***
适用GET提交数据，我们需要适用req.query提取
前端：
```
<form class="aaa" action="/about">
    <input type="text" name="name" value="">
    <button type="submit" name="button">button</button>
</form>
```
app.js 后台适用req.query.name来获取：
```
app.get('/about', function(req, res) {
  var info = [{name: 'Mary', age: 20},
  {name: 'Ben', age: 32},
  {name: 'Scotch', age: 21}
];
console.log(req.query.name);
	res.render('about', {
    info: info,
    title: "Information"
  });
});
```
***POST使用***
在post请求时，我们需要获取提交数据时，需要安装一个bodyParser的第三方库
npm install body-parser --save
在app.js 适用时需要添加：
var bodyParser = require('body-parser');
app.use(bodyParser.json({limit:"1mb"})); //body-parser解析json格式数据 有1mb的空间
app.use(bodyParser.urlencoded({    //此项必须在bodyParser.json下面，为参数编码
   extended:true
  }));
  将前端提交的数据经处理后变成json数据格式，所以可以直接用req.body.name,req.body.age来处理前端提交数据

/*******04-18*******************/  
Socket.io  
  什么是Socket.io？(实时响应)  
   它是一个实时应用提供跨平台实时通信的库。socket.io旨在使实时应用在每一个浏览器和移动设备上成为可能，模糊不同的传输机制间的差异  
  
   socket.io 是一个以实现跨浏览器、跨平台的实时应用为目的的项目。针对不同的浏览器版本或者不同客户端会做自动降级处理，选择合适的实现方式（websocket, long pull..），隐藏实现只暴露统一的接口。可以让应用只关注于业务层面上。   
  
   安装：npm install socket.io --save  
   在express适用socket.io创建文件app.js文件  
/******************************************/  
```
   var app = require('express')();  
   var server = require('http').Server(app);  
   var io = require('socket.io')(server);
   server.listen(3000);
   app.get('/',(req,res) =>{
     res.sendFile( __dirname + './index.html');
     });  // __diranme 什么意思！！！！！__ 似乎是可以接收到index.html的全部属性
   io.on('connertion',(socket) => {      //connertion 链接
       console.log()
       socket.emit('news',{hello:'world'}) //自己定义的news，后面的数据给它
       socket.on('other',(date) =>{
         console.log('收到数据'，data);
         });
     });
 ```
     后端的emit可以发送到前端的on事件里面        
     emit:用来发射一个事件，触发一个事件,第一个参数为事件名，第二个参数为要发送的数据，第三个参数为回调函数。  
     on:用来监听一个emit发射事件，第一个参数要监听的事件名，第二个参数为一个匿名函数用来接受对方发来的数据，该匿名函数的第一个参数为接收的数据，若有第二个参数，则为要返回的函数。  
      socket.io提供了三种默认事件：connect(链接成功触发)、message(发来数据触发)、disconnect(对方关闭链接后触发)。               
      socket.emit():向建立该链接的客户端广播  
      socket.broadcast.emit():向除去建立该链接的客户端的所有客户端广播  
      io.scockets.emit():向所有客户端广播，等于上面俩个和  
/******************************************/  
```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Demo socket.io</title>
  <script src="http://cdn.bootcss.com/socket.io/1.5.1/socket.io.min.js"></script>
  <script>
  var socket = io();
  socket.on('news', function(data){
    console.log("socket.on");
    console.log(data);
    socket.emit('other', { my: 'data'});
  });
  </script>
</head>
<body>
<h1>Welcome socket.io.</h1>

</body>
</html>
```
/**********************/
socket.io/demo/index.html  
客户端（这里是浏览器）通过引入 <script src="/socket.io/socket.io.js"></script>即可使用 socket.io 。var socket = io.connect('http://localhost'); 与 http://localhost 本地服务器建立连接并赋值给 socket 对象，如果是与其他服务器建立连接则只需将 connect() 参数修改为服务器的地址即可，这里 socket.io 客户端和服务器位于同一个服务器上，那么也可以简写为 var socket = io.connect(); 或是 var socket = io();  
**聊天室——主页面html**  
```
<!doctype html>
<html>
  <head>
    <title>Socket.IO chat</title>
    <style>
      * { margin: 0; padding: 0; box-sizing: border-box; }
      body { font: 13px Helvetica, Arial; }
      form { background: #000; padding: 3px; position: fixed; bottom: 0; width: 100%; }
      form input { border: 0; padding: 10px; width: 90%; margin-right: .5%; }
      form button { width: 9%; background: rgb(130, 224, 255); border: none; padding: 10px; }
      #messages { list-style-type: none; margin: 0; padding: 0; }
      #messages li { padding: 5px 10px; }
      #messages li:nth-child(odd) { background: #eee; }
    </style>
  </head>
  <body>
    <ul id="messages"></ul>
    <form action="">
      <input id="m" autocomplete="off" /><button>Send</button>
    </form>
    <script src="https://cdn.socket.io/socket.io-1.2.0.js"></script>
    <script src="http://code.jquery.com/jquery-1.11.1.js"></script>
    <script>
      var socket = io();
      $('form').submit(function(){
        socket.emit('chat message', $('#m').val());
        $('#m').val('');
        return false;
      });
      socket.on('chat message', function(msg){
        $('#messages').append($('<li>').text(msg));
      });
    </script>
  </body>
</html>
```
**聊天室后端nodejs负责通信**  
```
var app = require('express')();
var http = require('http').Server(app);
var io = require('socket.io')(http);

app.get('/', function(req, res){
  res.sendFile(__dirname + '/index.html');
});

io.on('connection', function(socket){
  socket.on('chat message', function(msg){
    io.emit('chat message', msg);
  });
});

http.listen(3000, function(){
  console.log('listening on *:3000');
});
___/
```
**广播消息**  
为了广播消息，你只需要简单地在emit和send方法之前加上broadcast标示符。广播意味着给所有人除了自己发送一条消息。  
  
***广播消息-服务端***  
```
var app = require('express')();
var http = require('http').Server(app);
var io = require('socket.io')(http);

app.get('/', function(req, res){
  res.sendFile(__dirname + '/index.html');
});

io.on('connection', function(socket){
  socket.broadcast.emit('broadcast');
  socket.on('chat message', function(msg){
    io.emit('chat message', msg);
  });
});

http.listen(3000, function(){
  console.log('listening on *:3000');
});

___/
```
***客户端***  
```
<!doctype html>
<html>
  <head>
    <title>Socket.IO chat</title>
    <style>
      #join { color: red;}
    </style>
  </head>
  <body>
    <div id="join"></div>
    <ul id="messages"></ul>
    <form action="">
      <input id="m" autocomplete="off" /><button>Send</button>
    </form>
    <script src="https://cdn.socket.io/socket.io-1.2.0.js"></script>
    <script src="http://code.jquery.com/jquery-1.11.1.js"></script>
    <script>
      var socket = io();
      $('form').submit(function(){
        socket.emit('chat message', $('#m').val());
        $('#m').val('');
        return false;
      });
      socket.on('chat message', function(msg){
        $('#messages').append($('<li>').text(msg));
      });
      socket.on('broadcast', function(msg){
        console.log('broadcast!');
        $('#join').append('<p><strong>Welcome to new friend.</strong></p>')
      })
    </script>
  </body>
</html>
```
  **发送和接收数据(并确认)**  
  有时，你可能在客户端确认接受到信息时获得一个反馈  
  为了座这件事儿，你只需要将一个函数作为.send 或者.emit方法的最后一个参数传递，另外，当你适用.emit时，你需要进行确认，这个以为着你还需要传送数据
  ```
  /———服务器端代码———/  
  var io = require('socket.io').listen(80);
  io.sockets.on('coonection',function(socket){
    socket.on('ferret',function(name,fn){
      fn('woot');
      });
    });
    /——客户端代码——/
    <script>
    var socket = io();
    socket.on('connect',function(){
      socket.emit('ferret','tobi',function(data){
        console.log(data);
        });
      });
      </scirpt>
```

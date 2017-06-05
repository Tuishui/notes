/*****04-12****************************************************************************************************************************/  
Node.js 官方网站 node.org 支持版本很多  
node 不是语言 也不是框架 也不是浏览器的库 只是一个平台 即时编译  
它可以将JavaScript 成为一种很快的语言 它跳过了Apache、Nginx  
语言特性与JavaScript相似  
Node 是一个框架似的平台，node核心 是V8引擎 (google为浏览器加快运行速度)  
       webkit （苹果公司）引擎 大部分浏览器都是用的这个，IE除外  
                   feesbook 空中wifi  
----------php python perl ruby ------------  
LAMP  
 L:linux操作系统 A:apache网络服务器 M:MySQL数据库 P:PHP/perl/Python 编程语言  
websaver(软件服务) php(开发语言) -× 整合用JS语言表达  
/*****************************************************/  
Node.js  
Node.js优点:  
(1).采用事件驱动、异步编程，为网络服务而设计  
(2).Node.js非阻塞模式的IO处理给Node.js带来在相对 低系统资源耗 用下的 高性能 与 出众的负载能力 ，非常适合作用依赖其他IO资源的中间层服务。  
(3).Node.js轻量高校，可以认为是数据密集型分布式部署环境下的实时应用系统的完美解决方案  

Node.js缺点:  
1.可靠性低  
2.单进程，单线程，只支持单核CPU，不能充分的利用多核CPU服务器。  
//一旦这个进程崩掉，那么整个web服务器九崩掉了。  

目前Node.js的网络服务器有以下集中支持多进程的方式:  
1.开启多个进程，每个进程绑定不同的端口，用反向代理服务器做负载均衡。  
           //好处是我们可以借助强大的Nginx做一些过滤检查之类的操作，同时能够实现比较好的均衡策略;但坏处是---我们引入了一个间接层。  
2.多个进程绑定在同一个端口侦听。  
3.一个进程负责监听、接受链接，然后把接收到了链接平均发送到子进程中去处理。  
/*****************************************************/  
 异步式 i/o 与事件驱动  
 Node.js最大特点就是采用异步式 I/O 与事件驱动的架构设计。  
 对于高发的解决方案，传统的架构是多线程模型，也就是为每个业务逻辑提供一个系统线程，通过系统线程切换来弥补同步式i/o调用时的事件开销。。  
/********************************************/  
//文件句柄:就是对文件操作时，文件给予的响应或者是反馈  
“py之open函数” 对文件只有“读” “写” “读-写”  
stdin = 0 输入； stdout = 1 输出 stderr = 2 错误  
cluster 官方的库  bios:配置好所有硬件的地址空间  

node.js 安装方法  （安装版本 v6.10.2）  
cur -sl https//deb.nodesource.com/setup_6.x| sudo -E bash - 安装源  
sudo apt-get install -y nodejs  
删除命令: sudo apt-get....未写完  
开发环境安装:sudo apt-get install -y build-essential  
/******************/  
npm包管理node第三方安装包 （node.js它有自己的包 也有第三方包）  

/****************************************/  
nvm 专门管理node版本   
nvm 安装方法： curl-o-https://raw.githubusercontent.com/creationix/nvm/v0.30.2/install.sh | bash  
vim .bashrc 查看最下面的有没有  

export NVM_DIR="$HOME/.nvm"  
[ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh" # This loads nvm  
. ./. bashrc 编译器  
node --version  
nvm install v6.10.2  
详细 操作请看nvm 说说明书  
/**************************************/  
npm  
npm install express 本地安装  
npm install express -g 全局安装  
npm install <packageName> --force 强制重新创建安装  
npm unpdate <packageName> 更新已经安装的模块  

node 兼容性很差，每次都在做升级  

npm install 读出第三放包 再安装 (package.json)  
npm install express --save 把express第三方文件名字 保存到  
package.json  
npm init 建立 package.json 文件  

假如你不知道 源文件名字 或者 源文件名字太长 那么你可以使用以下方法  
  在package.json 文件之中 的test后面的一行 放这样"start":"node 文件名.js"  
  在终端运行 写入代码 npm run start 可以自动运行  
    运行显示： > demo@1.0.0 start /home/linux/nodejs/demo  
             > node demo.js  

  shift+zz 快速保存推出  
// 假如 运行 npm run start 后 退出 按ctrl+z 退出  
  那么这个状态是在后台运行 此时应该 fg 唤醒 然后在 ctrl+c 推出  
  
"script":{ //可以执行多个代码  
  "preinstall":"echo here it comes!",  
  "postinstall":"echo there it goes",  
  "start":"node index.js",  // 必须写  
  "test":"tap test/*.js"  
}
/********************//  
/-----------异步i/o与事件式编程----------------/  
/****04-11**************************************************/  
阻塞:i/o  
非阻塞:  
px 查看相关的进程  
top 运行程序 占CPU 多少  // sorg 是整个ubuntu的界面  
console.error(err); // 打印错误  
/**********************/  
什么是阻塞，什么是非阻塞  
阻塞:阻塞i/o的特点是，调用之后一定要等到系统内核层面完成所有的事件操作，调用结束。  
非阻塞i/o和阻塞i/o最大的区别就是 （内核提供了非阻塞i/o）非阻塞i/o调用之后会立即返回，返回之后，cpu的时间片可以用来处理其他事物，此时cpu性能明显提升。  
非阻塞弊端:应为完整的i/o没有完成，所以为了获取完整i/o要进行轮询。  
/************************/  
什么是异步i/o？  
异步i/o就是i/o提交给系统，让系统替你做，做完之后再用某种方式通知你，此时操作系统已经帮你完成i/o操作。  
什么是非阻塞i/o？  
非阻塞i/o就是通过某中方式不定时的想系统做某个轮询，当开始后，是自己完成i/o。  
/******************************/  
什么是事件模型？  
大多数Node.js核心API都采用管用的异步事件驱动架构，其中某些类型对象会周期性地触发命名事件来调用函数对象。  
/*****************************/  
node循环机制图:  
    事件循环 -> 回调函数->回调函数方法->事件队列->事件循环  
                  L->事件循环  
  

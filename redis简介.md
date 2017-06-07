##ububtu 安装 Redis
 **2017-06-07**  
 更新安装源，安装编程工具tcl  
 ```
 sudo apt-get updatae  
 sudo apt-get install build-essential tcl
 ```
 下载redis源码包  
 通过curl下载最新的redis源码压缩文件，如果没有安装curl命令工具 先行安装它。  
 ```
 sudo apt-get install curl -y
 curl -O http://download.redis.io/redis-stable.tar.gz
 ```
 解压redis  
 解压刚刚下载的redis安装包  
 ```
 tar xzvf redis-stable.tar.gz
 ```
 编译redis  
 进行解压目录中，使用make命令编译redis
 ```
 cd redis-stable
 make
 ```
 进行测试
 ```
 make test
 ```
 redis 安装
 ```
 sudo make install
 ```
 配置redis  
 需要/etc目录下创建一个redis目录，用来保存配置文件
 ```
 sudo mkdir /etc/redis
 ```
 复制配置文件  
 将redis-stable 目录下中的redis.conf默认的配置文件复制到/etc/redis目录中
 ```
 sudo cp redis-stable/redis.conf  /etc/redis
 ```
 **修改编辑redis.conf文件**   
 需要打开supervised和设置存储临时数据目录   
 需要将supervised设置为systemd
 ```
 sudo vim /etc/redis.conf
 ```
 ```
# If you run Redis from upstart or systemd, Redis can interact with your
# supervision tree. Options:
#   supervised no      - no supervision interaction
#   supervised upstart - signal upstart by putting Redis into SIGSTOP mode
#   supervised systemd - signal systemd by writing READY=1 to $NOTIFY_SOCKET
#   supervised auto    - detect upstart or systemd method based on
#                        UPSTART_JOB or NOTIFY_SOCKET environment variables
# Note: these supervision methods only signal "process is ready."
#       They do not enable continuous liveness pings back to your supervisor.
supervised systemd
 ```
 接下来，去设置下临时数据的存储目录为 /var/lib/redis, ./var/lib/redis 这是目录需要自己去创建  
 ```
# The working directory.
#
# The DB will be written inside this directory, with the filename specified
# above using the 'dbfilename' configuration directive.
#
# The Append Only File will also be created inside this directory.
#
# Note that you must specify a directory here, not a file name.
dir /var/lib/redis
 ```
 创建systemd配置文件   
 需要创建 /etc/systemd/system/redis.service配置文件  
 ```
 sudo vim /etc/systemd/system/redis.service
 ```
 编辑如下内容：  
```
[Unit]
Description=Redis In-Memory Data Store
After=network.target

[Service]
User=redis
Group=redis
ExecStart=/usr/local/bin/redis-server /etc/redis/redis.conf
ExecStop=/usr/local/bin/redis-cli shutdown
Restart=always

[Install]
WantedBy=multi-user.target
```
创建redis用户，组和目录  
创建redis用户，这个用户不需要创建目录  
```
sudo adduser --system --group --no-create-home redis
```
创建刚才配置文件中，使用/var/lib/redis 目录
```
sudo mkdir /var/lib/redis
```
将redis用户和组分配到/var/lib/redis目录
```
sudo chown redis:redis /var/lib/redis
sudo chmod 770 /var/lib/redis
```
**启动测试redis服务**    
启动redis服务
```
sudo systemcti start redis
```
查看redis服务启动是否成功   
```
sudo systemcti status redis
```
运行下面的命令，将会有下面的输出信息：
```
Output
● redis.service - Redis Server
   Loaded: loaded (/etc/systemd/system/redis.service; enabled; vendor preset: enabled)
   Active: active (running) since Wed 2016-05-11 14:38:08 EDT; 1min 43s ago
  Process: 3115 ExecStop=/usr/local/bin/redis-cli shutdown (code=exited, status=0/SUCCESS)
 Main PID: 3124 (redis-server)
    Tasks: 3 (limit: 512)
   Memory: 864.0K
      CPU: 179ms
   CGroup: /system.slice/redis.service
           └─3124 /usr/local/bin/redis-server 127.0.0.1:6379       

```
redis命令行工具  
可以使用命令工具，链接redis  
```redis-cli
```
```
127.0.0.1:6379>info
```
运行redis
```
src/redis-server
```
参考文献  
https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-redis-on-ubuntu-16-04
ubuntu 1604安装配置redis

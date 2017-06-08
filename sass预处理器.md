##安装sass  
###第一步：安装Ruby  
sass是用Ruby语言写的，但是俩这的语法没有任何关系，所以学Sass不用学Ruby，只是必须先安装Ruby，然后在安装Sass  
其中，linux和Mac已经自带Ruby，不用再安装。Windows用户可以
从此处下载@https://www.ruby-lang.org/en/documentation/installation/  
验证Ruby是否安装成功
```
ruby -v
```
或者  
```
ruby --version
```
如果输出Ruby版本号，则表示安装成功  
***************************************************************
###第二步，安装Sass  
在命令行输出下面的命令  
```
gem install sass
```
这样Sass就安装成功了。检测是否安装成功
```
sass -v
```
或者
```
sass --version
```
如果输出Sass版本号，则表示安装成功  
可以使用以下命令更新Sass版本
```
sudo gem update sass
```
###第三步，运行Sass  
```
sass input.scss out.css
```
```
sass --watch input.sass:out.css
```
```
sass --watch app/sass:public/stylesheets
```

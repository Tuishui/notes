 /****04-05*********************************************************************************************/
01.git

备注：outlook.com 申请一个邮箱
     如果不用QQ邮箱 git 会鄙视你....

ls -al 查看隐藏 目录

tuishui@outlook.com
yuanhui_123
outlook邮箱


git笔记

mkdir git   建立一个git 文件  
git init    进行初始化本地仓库     查看git 仓库位置  
ls -al       查看仓库内容 显示 .git 文件  
touch hello.html     创建一个html 文件  
git status 查看当前文件下/仓库下 的文件状态  
      此时我们需要把次文件做一些操作  
git add .       关注当先文件名字 如果多的化加一个. .表示 当前目录下 次代码 表示 git 到当前目录下  
git status      查看当前目录下所有文件 此时 文件颜色为绿色  
git config --global user.name ""       编辑你自己的名字  
git config --global user.email ""      编辑你自己的邮箱  
git config --global user.editor vim      把核心改成 vim  
git commit         查看当前提交下目录信息 文件  
git commit --amend     返回那个提交文件  
git log  查看该 提交文件  
    commit dc40fc..........    commit ID 哈希值 ID唯一  
    Author : shui Tui <Tuishui@outlook.com>
    Date: wed Apr 5 10:49:54 2017 +0800

    Init commit 初始化提交
    (标题)
    (内容)Add new files . 新的一个文件



scp 网络之间的cope
  scp IP地址 用户名 linux@192.168.168.1.111: ~(+目录下的路径)/a.c .

untranked 文件没有被加入到版本库
 git add .
 unmodified 文件未被修改过
  vi编辑 或者是 ”atom“        修改之后必须加入git add  否则:git commit -a
 modified 文件已经被修改过了

 staged 准备号，可以提交到版本库之中了

 如果一不小心删除的话
 可以使用 git checkout hello.html (必须git commit)

 git reset --hard 哈希值 回到这个版本
  cat hello.html 看一下 hello.html 文件
  git diff  查看修改 命令的祝福

touch .gitignore 忽略文件 以及目录

git stash 暂存 显示目录
 git stash save  暂存
 git stash show  暂存 内容

 Emacs   Richard stallman//人名   gnu.org

 /*****04-06********************************************************************************************/
新的一天早已开始，那我们还在等待什么～  
. 当前目录  
.. 上一级目录  
* 一个文件  
? 一个位置上的随机数  
   什么是patch!  
   patch: 补丁 在这里多指程序中的bug 需要我们进行fixed  fixed 源码文件就是patch 实际就是保存俩个文件的差异  
   patch 怎么生成 : git format-patch  -p1  
   打开patch : git am patch-name  
  
  工作流  
  Tag 自己看  
  git branch -av   查看分支 一般默认分支master  
  git branch develop  创建分支 develop  
  git checkout develop 切换分支  
  git branch -D branch-name 删除分支  
  git checkout master 先去master分支上然后 再合并 / git merge develop 合并分支(如果出现冲突的时候可以适用 git mergetool 解决冲突)  

  tag 标签信息  
  git tag 显示所有标签  
  git tag 哈希值 创建标签  
  git log  --decorate 可以显示包含标签历史资料  
  git log tag-name 显示tag开始的所有提交信息  
  git show tag-name 可以显示tag的信息和提交的内容以及patch  
  git checkout -b branch-name tag-name 可以更具tag 的标记进行创建分支  
  git tag -d <tagname> 删除tag标签  
     github.com 和 bitbuckbet.org  
       github 个人开发私有库 你将花钱一个月7美金  
       bitbuckbet 5个人合作花钱  
  
  git clone https// 下载  
  git push -u origin master (回车以后会输出名字和密码)上传到github 文件  
 /*****04-07********************************************************************************************/
  服务器
  git push origin master 同步moaster分支  
  git push origin branch-name 同步其他分支  
  git push origin origin --tags 同步标签  
  git push -u origin :branch-name 删除远程分支  
  git push origin --delete <branchName>  
  git push origin --delet tag <tagname>删除远程分支  
  git clone url 下载远程仓库  
  git pull 当前在哪里 同步哪里的分支  

  本地  
  git checkout -b new 哈希值     把此次 提交 放到 new 分支里面 而且切换到new 分支  

  创建html文档在  

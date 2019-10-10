# 目录

- []()
- [基本操作]()
  - [git的公共配置]()
  - [创建/获取本地仓库]()
  - [查看/修改远程仓库]()
  - [分支管理]()
- [工作流程]()
- [参考资料](#参考资料)

## 1. git是什么

Git是一个基于C语言开发、开源的分布式版本控制系统，用于敏捷高效地处理任何或小或大的项目。
对于程序员它可以是代码管理工具。
对于小白它可以是网盘。

> git的作者同时也是linux的作者Linus Torvalds([github](https://github.com/torvalds))! Git的开发初衷是为了帮助社区管理Linux内核开发。

## 2. git和svn的区别

1. Git是分布式的，SVN不是：详见[集中式与分布式版本控制系统](集中式与分布式版本控制系统.md)最明显的特征就是git不依赖网络就可以查看所有历史版本、创建项目分支。

2. Git把内容按元数据方式存储，而 SVN是按文件：所有资源控制系统(集中式和分布式)都是把文件的元信息隐藏到一个以`.`开头的文件夹里(如git存放到.git中)。`.git`的体积远远大于`.svn`，因为存储着中心版本的所有版本的所有东西，如标签、分支、版本记录等

3. Git分支和SVN的分支不同：git的分支管理更加简单方便。

4. Git没有全局的版本号，SVN有：❓存疑，git拥有SHA-1标识，而且还可以创建tag

5. Git的内容完整性要优于SVN：GIT的内容存储使用的是SHA-1哈希算法。这能确保代码内容的完整性，确保在遇到磁盘故障和网络问题时降低对版本库的破坏❓待确认

## 3. 常见Git仓库

### 3.1 Github

### 3.2 Gitlab

### 3.3 码云(gitee)

## 4. 工作区、暂存区、版本库

## 5. 基本操作

### 5.1 git的公共配置

```
# 注意尖括号里的需要改成自己的信息
$ git config --global user.name '<your name>'
$ git config --global user.email '<your email>'
```

### 5.1 创建/获取本地仓库

如果没有远程仓库，则在本地项目文件夹中执行
```
# 初始化项目仓库
$ git init

# 添加远程仓库
$ git remote add origin git@xxx:xxxx
```
如果有远程仓库，则从远程仓库下载到本地
```
# 使用https协议
$ git clone https://xxxxx

# 使用ssh协议
$ git clone git@xxx:xxxx
```

### 5.2 查看/修改远程仓库
⚠️注意任何git命令在不指定远程仓库名称/地址的时候，默认远程仓库使用origin
```
# 查看帮助
$ git remote help

# 查看所有远程仓库的名称
$ git remote

# 查看所有远程仓库及其fetch和push的地址
$ git remote -v

# 添加远程仓库
$ git remote add <仓库名称> <仓库地址>

# 删除远程仓库
$ git remote remove <仓库名称>
```

## 参考资料

- [Git官网](https://git-scm.com/)
- [菜鸟教程 - Git](https://www.runoob.com/git/git-tutorial.html)
- [廖雪峰 - Git](https://www.liaoxuefeng.com/wiki/896043488029600)
- [oschina - 红薯 - git和svn之间的五个基本区别](https://www.oschina.net/news/12542/git-and-svn)
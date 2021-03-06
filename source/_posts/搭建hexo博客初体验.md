---
title: 搭建Hexo博客初体验
date: 2018-06-02 18:49:11
photos: "https://i.imgur.com/qwUokyx.png"
tags: Github
categories: Github
---
# 摘要： #
这是一篇关于小白如何使用Github Pages和Hexo搭建属于自己的博客：

1. 如何使用和配置Hexo框架
2. 如何将Hexo部署到自己的github项目中


# 前言： #
很久之前早就想弄一个自己的博客，但是迟迟没有落实，大概是一直没有找到自己想要的那种博客（借口~），今天看了stormzhang公众号的一篇文章《我为什么坚持写博客？》推荐的hexo，上网了解了下发现这大概就是我想要的吧~经过一下午折腾终于搭建属于自己的博客，我觉得很有必要把整个过程写下来分享给大家互相学习使用。不废话了直奔主题！
#   一、环境配置   #
**安装node.js**

[下载node.js](https://nodejs.org/en/download/)
选择自己电脑版本的
![](https://i.imgur.com/PObCNrt.png)
本人是windows 64位，直接傻瓜式下载使用即可

**安装git**

[下载git](https://git-scm.com/download/win)
同样是根据电脑版本下载

下载完成，通过在命令行输入 git version 查看是否安装成功，有输出版本号说明安装成功。

鼠标邮件菜单里就多了Git GUI Here和Git Bash Here两个按钮，一个是图形界面的Git操作，一个是命令行，我们选择Git Bash Here。

![](https://i.imgur.com/6rlZnbr.png)
![](https://i.imgur.com/xo1kjnh.png)
# 二、Hexo安装 #
①桌面鼠标右键，选择Git Bash Here，输入下面命令：

    npm install -g hexo-cli

如果出现![](https://i.imgur.com/5i33liB.png)
说明hexo已经安装成功（针对windows）

②然后需要创建一个文件夹来存放hexo文件（相当于你的博客文件夹）
例如：我在电脑上手动创建了一个名叫blog的文件夹，然后需要执行以下命令初始化：

    hexo init e:\blog
进入该目录：

    cd e:\blog
执行以下命令，系统会可以根据package.json文件中dependencies的配置安装所有依赖包：

    npm install
然后生成部署文件，启动本地服务

    1.hexo g # hexo generate, 生成静态文件
	2.hexo s # hexo server，可以在http://localhost:4000/ 查看 

其他hexo命令用法可参考 [Hexo官网](https://hexo.io/zh-cn/docs/commands.html)

接下来我们可以在本地预览自己的博客了，打开[http://localhost:4000/](http://localhost:4000/)
![](https://i.imgur.com/nTBog0f.png)
# 三、Github Pages配置 #
顾名思义需要一个Github账号，然后创建一个仓库：
![](https://i.imgur.com/QUPRsyk.png)
<font color=#A52A2A size=4 > 

注意：仓库的名字必须是username/username.github.io

注意：仓库的名字必须是username/username.github.io

注意：仓库的名字必须是username/username.github.io

</font>
例如：我的用户名为jefff8,那么Repository name必须命名为：jefff8.github.io

重要的事情说三遍！！！（当初踩过的坑...）

**配置SSH密钥**

上传文件需要配置ssh key，所以首先需要检查本机电脑是否已经存在SSH keys，如果存在删除 .ssh文件夹里面的所有文件（如果不存在的忽略这条）

![](https://i.imgur.com/zPoz1X3.png)
然后设置下name和email

    `git config --global user.name "<your name>"`
	`git config --global user.email "<your email>"`

name的名字随便起，email我建议填github同一个邮箱

**生成SSH密钥**

输入以下命令生成，邮箱是github里面注册的邮箱，ok回车：

    `ssh-keygen -t rsa -C "XXXXX@qq.com"`

一路按回车键即可，如果设置了密码请记住。 
这一步在~/.ssh/下生成了两个文件id_rsa 和 id_rsa.pub

**获取SSH密钥**

	`$ cat ~/.ssh/id_rsa.pub`

新建一个key，然后拷贝下生成的key
![](https://i.imgur.com/z3CpzEt.png)
key粘贴刚刚生成的密钥，title随便起

<font color=#A52A2A >注意：重点圈起来，key下面的√记得一定要打哦！不然后面会报错，又是踩过的坑说多都是泪...</font>

提交后，输入一下命令：

    ssh git@github.com

如果出现这样的内容：

    The authenticity of host 'github.com (192.30.252.128)' can't be established.
	RSA key fingerprint is 16:27:ac:a5:76:28:2d:36:63:1b:56:4d:eb:df:a6:48.
	Are you sure you want to continue connecting (yes/no)? yes
	Warning: Permanently added 'github.com,192.30.252.128' (RSA) to the list of known hosts.
	Hi git-xuhao! You've successfully authenticated, but GitHub does not provide shell access.
	Connection to github.com closed.

大致恭喜你配置成功！！
这时钥匙也变绿啦![](https://i.imgur.com/TNkGnwi.png)
# 四、部署到Github #
**配置_config.yml**

- 编辑刚刚新建的文件夹（e:/blog）根目录内,找到该文件，找到并修改Deployment部分（一般在最后）![](https://i.imgur.com/KvdFomt.png)

![](https://i.imgur.com/BHTHcP8.png)
注意：在每个填入前加个空格(否则会有错误)，其中repository填的是刚刚github新建仓库的SSH地址。

- 安装Git包，执行以下命令：

	    npm install hexo-deployer-git --save

- cd到根目录，执行以下命令即可：

	    hexo g
    	hexo d
now，你可以输入[https://username.github.io](https://username.github.io)来访问自己的博客啦（开森）！！！


# 五、关于Hexo使用 #
**①更换主题**

可以进入[Hexo官网主题专栏](https://hexo.io/themes/)找到自己想要的主题（个人强推：next）
![](https://i.imgur.com/o5mCSms.png)


找到想要的然后到克隆主题啦，十分简单，复制github地址输入一下命令：

    git clone https://github.com/iissnan/hexo-theme-next(此处地址替换成你需要使用的主题的地址)
成功后，你会发现themes文件夹里面多了一个注意文件夹![](https://i.imgur.com/haazSiB.png)

然后修改下根目录配置文件_config.yml里面的theme：主题名字（主题文件夹名字相同）
![](https://i.imgur.com/QnjowPl.png)

重新部署主题，Git Bash cd到根目录，输入一下命令：

    hexo g
	hexo s #本地预览
如果满意，就可以输入一下命令上传：

    hexo d
**②新建博客文章**

新建一篇文章(md文件)输入以下命令：

	hexo n "文章标题"
然后会在根目录/source/_posts 下生成你的文章文件，打开编辑器编辑就好（本人使用：MarkdownPad 2）![](https://i.imgur.com/6PE34WM.png)

编写好后只要执行：

    hexo d -g
就会更新我们的Github库。

有关更多配置使用问题，可以参考[Hexo官网文档](https://hexo.io/zh-cn/docs/) ~

---
title: "Linux中的文本"
date: 2023-03-07T16:17:35+08:00
draft: true
---

### 几个对研究Linux系统有帮助的命令
* ls 列出目录内容
* file确定文件类型
* less浏览文件内容

其中ls可以列出多个指定目录的内容

	wangxiaoyudeMacBook-Pro:~ wangxiaoyu$ ls ~ /usr
	/Users/wangxiaoyu:
	AndroidStudioProjects    Music            node_modules
	Applications        Pictures        package-lock.json
	Desktop            Public            projects
	Documents        Training-ground        self
	Downloads        depends            北航论文
	Library            document
	Movies            learn
	
	/usr:
	X11        bin        libexec        sbin        standalone
	X11R6        lib        local        share
	
上面的例子列出了用户家目录（字符～表示）和/usr目录的内容

ls -l 改变输出格式，来得到更多的细节

	wangxiaoyudeMacBook-Pro:~ wangxiaoyu$ ls -l
	total 240
	drwxr-xr-x    3 wangxiaoyu  staff      96 10 31 14:58 AndroidStudioProjects
	drwx------@   5 wangxiaoyu  staff     160  7 19  2019 Applications
	drwx------@  10 wangxiaoyu  staff     320  1 30 19:21 Desktop
	drwx------@  44 wangxiaoyu  staff    1408  1 31 10:16 Documents
	drwx------@ 150 wangxiaoyu  staff    4800  1 30 12:42 Downloads
	drwx------@  80 wangxiaoyu  staff    2560 10 31 14:36 Library
	drwx------+   5 wangxiaoyu  staff     160  1  5 23:12 Movies
	drwx------+   5 wangxiaoyu  staff     160 10 10 22:05 Music
	drwx------+   5 wangxiaoyu  staff     160 11  8 22:24 Pictures
	drwxr-xr-x+   6 wangxiaoyu  staff     192 12  7 10:14 Public
	drwxr-xr-x    7 wangxiaoyu  staff     224  1 29 20:29 Training-ground
	drwxr-xr-x    9 wangxiaoyu  staff     288  1 30 19:21 depends
	drwxr-xr-x    7 wangxiaoyu  staff     224  1 30 12:27 document
	drwxr-xr-x   22 wangxiaoyu  staff     704  1 27 19:54 learn
	drwxr-xr-x   45 wangxiaoyu  staff    1440 12  7 10:13 node_modules
	-rw-r--r--    1 wangxiaoyu  staff  120424 10 19 12:43 package-lock.json
	drwxr-xr-x   18 wangxiaoyu  staff     576  1 30 12:31 projects
	drwxr-xr-x   15 wangxiaoyu  staff     480 11 12 10:06 self
	drwxr-xr-x   17 wangxiaoyu  staff     544  1 17 14:57 北航论文
使用ls命令的 -l 选项，则结果以长模式输出。

### 选项和参数
大多数的命令看起来像是这样

	command -options arguments
大多数命令使用的选项，是由一个中划线加上一个字符，例如 ‘-l’但是许多命令，包括来自GNU项目的命令，也支持长选项，长选项由两个中划线加上一个字（单词）组成。也有许多命令允许把多个的短选项串在一起使用，例如: ls -lt

‘l’选项产生长格式输出，’t’选项按文件修改时间的先后来排序。
### 深入研究长格式输出

	wangxiaoyudeMacBook-Pro:~ wangxiaoyu$ ls -l
	total 240
	drwxr-xr-x    3 wangxiaoyu  staff      96 10 31 14:58 AndroidStudioProjects
	drwx------@   5 wangxiaoyu  staff     160  7 19  2019 Applications
	drwx------@  10 wangxiaoyu  staff     320  1 30 19:21 Desktop
	drwx------@  44 wangxiaoyu  staff    1408  1 31 10:16 Documents
	drwx------@ 150 wangxiaoyu  staff    4800  1 30 12:42 Downloads
	drwx------@  80 wangxiaoyu  staff    2560 10 31 14:36 Library
	drwx------+   5 wangxiaoyu  staff     160  1  5 23:12 Movies
	drwx------+   5 wangxiaoyu  staff     160 10 10 22:05 Music
	drwx------+   5 wangxiaoyu  staff     160 11  8 22:24 Pictures
	drwxr-xr-x+   6 wangxiaoyu  staff     192 12  7 10:14 Public
	drwxr-xr-x    7 wangxiaoyu  staff     224  1 29 20:29 Training-ground
	drwxr-xr-x    9 wangxiaoyu  staff     288  1 30 19:21 depends
	drwxr-xr-x    7 wangxiaoyu  staff     224  1 30 12:27 document
	drwxr-xr-x   22 wangxiaoyu  staff     704  1 27 19:54 learn
	drwxr-xr-x   45 wangxiaoyu  staff    1440 12  7 10:13 node_modules
	-rw-r--r--    1 wangxiaoyu  staff  120424 10 19 12:43 package-lock.json
	drwxr-xr-x   18 wangxiaoyu  staff     576  1 30 12:31 projects
	drwxr-xr-x   15 wangxiaoyu  staff     480 11 12 10:06 self
	drwxr-xr-x   17 wangxiaoyu  staff     544  1 17 14:57 北航论文
	
### 确定文件类型
用file命令来确定文件类型，当调用file命令后，file命令会打印出文件内容的简单描述例如：

	file picture.jpg
	
	picture.jpg: JPEG image data, JFIF standard 1.01
有许多类型的文件，事实上在Linux中，有个普遍的观念是“一切皆文件“有一些文件格式不太常见，极少数文件相当陌生。

less 命令是一个用来浏览文本文件的程序，Linux系统，有许多人类可读的文本文件。less程序为我们检查文本文件提供了方便。
### 什么是文本
在计算机中，有很多方法可以表达信息。所有的方法都涉及到在信息与一些数字之间确立一种关系，而这些数字可以用来代表信息。毕竟，计算机只能理解数字，这样所有的数据都被转换成数值来表示。

文本是简单的字符与数字之间的一对一映射，非常紧凑，五十个字符的文本翻译成五十个字节的数据。文本只是包含简单的字符到数字的映射，理解这一点很重要。它和一些文字处理器文档不一样，比如说微软word文档，这些文件和简单的ASCII文件形成鲜明的对比，它们包含非常多文本元素来描述它的结构和格式。

### 为什么文本很重要
许多包含系统设置的文件—配置文件，是以文本格式存储的，许多系统所用到的实际程序—-脚本，也是这种格式存储的。

### Less is More
less 程序是早期Unix程序more的改进版，less这个名字，对于习语“less is more” 开了个玩笑，这个习语也是现代主义建筑师和设计者的座右铭。
less允许前后翻页，more只能向前翻页
### 旅行指南/文件布局
Linux系统中，文件系统布局与类Unix系统的布局很相似，实际上，一个已经发布的标准，叫做Linux文件系统层次标准，详细说明了这种设计模式。不是所有的Linux发行版都根据这个标准，但大多数都是。
### 符号链接/软连接
描绘一下这样的情景：一个程序要求使用某个包含在名为“foo”文件中的共享资源，但是“foo”经常改变版本号。 这样，在文件名中包含版本号，会是一个好主意，因此管理员或者其它相关方，会知道安装了哪个“foo”版本。 这会导致另一个问题。如果我们更改了共享资源的名字，那么我们必须跟踪每个可能使用了 这个共享资源的程序，当每次这个资源的新版本被安装后，都要让使用了它的程序去寻找新的资源名。 这听起来很没趣。这就是符号链接存在至今的原因。比方说，我们安装了文件 “foo” 的 2.6 版本，它的 文件名是 “foo-2.6”，然后创建了叫做 “foo” 的符号链接，这个符号链接指向 “foo-2.6”。 这意味着，当一个程序打开文件 “foo” 时，它实际上是打开文件 “foo-2.6”。 现在，每个人都很高兴。依赖于 “foo” 文件的程序能找到这个文件，并且我们能知道安装了哪个文件版本。 当升级到 “foo-2.7” 版本的时候，仅添加这个文件到文件系统中，删除符号链接 “foo”， 创建一个指向新版本的符号链接。这不仅解决了版本升级问题，而且还允许在系统中保存两个不同的文件版本。 假想 “foo-2.7” 有个错误（该死的开发者！），那我们得回到原来的版本。 一样的操作，我们只需要删除指向新版本的符号链接，然后创建指向旧版本的符号链接就可以了。

有点类似于一个文件的快捷方式，上层的程序调用快捷方式，快捷方式指向真正的运行程序。
还有一种硬链接，同样允许文件有多个名字，但是硬链接以不同方法来创建多个文件名。


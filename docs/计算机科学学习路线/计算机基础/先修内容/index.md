# 先修内容

~~还未完善的页面~~

## 提问
提问的智慧这篇文章的内容固然重要，私以为一开始拿出来很没有必要，它的不友好程度甚至能掐灭刚刚燃起的火种。我更鼓励在经过自己尝试后再去问别人，就算不能百分之百达到“提问的智慧”，但是起码你经过了自己的思考。

在向别人求助时，请尽可能的描述好这个问题，以及问题出现的背景或是上下文，如果你仅仅是问一句“为什么我装不上java”诸如此类的问题，我相信大部分人都会认为你是一个讨厌的寄生虫。所以请尽可能的描述好你的问题，你可以附上一些图片来更好的解释问题。哦对，别忘了感谢帮助了你的人，因为他们本没有义务。

提问前都会遇到一个想法：问这个合不合适？面对这个问题，我可能不会写太多，以前怕麻烦别人，现在即  使很easy/不该问的问题，丢给GPT都可以给你答复。所以，你会主动提问吗？

## 工具

如果你对下面的内容没有概念，请自行了解，或是学习[计算机教育中缺失的一课](https://missing-semester-cn.github.io).

### Git
很多课程都需要Git进行文件的版本管理，而这些都会在一开始教你基础的语法。

你也可以通过一些文档实操入手，不用学的太深入，到最后都是现用现查(对我来说是这样的)。有个Up推荐给大家：GeekHour，他的Git教程做的很好。

在做后续课程CS61B-21Sp的时候你将有机会更深入的了解git的工作原理.

初期唯一的学习建议是不要从命令入手，而是从文件的工作区域及状态了解

### MarkDown
找到一个合适的编辑器多学多用，不要提Word谢谢喵

这里推荐几个有名的:Vscode(编辑器),Typora（编辑器）,Notion（云端笔记）,Obsidian（本地笔记/知识库）

### Linux/Shell
拥有一个Linux环境在CSer内应该见怪不怪，尽早安装并上手吧(我用的是双系统：Win+Wsl，主要用Mac)

学会使用命令行也是不可缺少的技能

推荐Missing Semester这门课，内容确实不错，B站也有专门翻译的视频，0xFFFF论坛也进行了这个系列的学习讨论，可以参考

### 搜索引擎
前情提要：本站所有“Google一下”，都是“使用搜索引擎搜索一下”的代词

将默认搜索引擎更换成Google...(没有Baidu别想了)是必须的，这几乎决定了你你能够获取的信息密度以及精确度，在Google不了的情况下，请用bing来替代，而不是baidu.

当然Baidu也有其适用的范围，所以不能一板拍，比如查一些马原题目还是可以用的

### VPN

～～自行Google～～因为没有vpn你甚至无法Google，所以可以试试用Bing了解相关信息，本指南不提供科学上网教材（报名

## 环境配置

个人看来，环境配置是计算机初学者很容易忽略的一个部分，但环境却至关重要，有很多问题其实都源自环境。

如果你是Windows用户，在所有的工作开始之前，必须强调一点非常重要的事情，在设置**Windows用户名**的时候，一定要设置成**英文**,因为中文经常会出现一些奇怪的错误，同理在安装一些软件的时候，目录最好也要是中文。

如果你是 Mac 用户，那么你很幸运，这份[指南](https://sourabhbajaj.com/mac-setup/) 将会手把手地带你搭建起整套开发环境。如果你是 Windows 用户，在开源社区的努力下，你同样可以获得与其他平台类似的体验：[Scoop](https://github.com/ScoopInstaller/Scoop)。

### 包管理

首先我们需要了解一个概念——包管理，在环境配置中使用包管理工具可以极大程度地减少可能会出现的问题，

??? note "那么什么是包管理呢？"
    包管理工具是用于自动安装、升级、配置和移除软件包的系统。在不同的操作系统上，包管理工具可以帮助用户更方便地管理软件依赖和版本，大大简化了软件的安装和维护过程。

下面是Windows和Macos常用的包管理工具的安装教程
#### Homebrew(Macos)

[官网](https://brew.sh)

只需要打开你的终端，输入

```shell
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

脚本就会自动执行安装配置

以上时官网提供的安装教程，但是对于处在国内网络环境下的我们，还有一种更便捷的方法，感谢这个[本地化仓库](https://github.com/cunkai/HomebrewCN)

```shell
/bin/zsh -c "$(curl -fsSL https://gitee.com/cunkai/HomebrewCN/raw/master/Homebrew.sh)"
```

安装方法是一样的，但这个版本是国人制作的更适合中国宝宝体质的homebrew安装脚本，会自动配置好镜像源（如果你不知道镜像源这个概念，可以自行Google一下）。

#### Scoop(Windows)

[官方文档](https://github.com/ScoopInstaller/Scoop)

Scoop 需要 [Windows PowerShell 5.1](https://aka.ms/wmf5download) 或者 [PowerShell](https://aka.ms/powershell) 作为运行环境，如果你使用的是 Windows 10 及以上版本，Windows PowerShell 是内置在系统中的。而 Windows 7 内置的 Windows PowerShell 版本过于陈旧，你需要手动安装新版本的 PowerShell。

> 由于发现很多同学在设置 Windows 用户时使用了中文用户名，导致了用户目录也变成了中文名。如果按照 Scoop 的默认方式将软件安装到用户目录下，可能会造成部分软件执行错误。所以这里推荐安装到自定义目录，如果需要其他安装方式请参考： [ScoopInstaller/Install](https://github.com/ScoopInstaller/Install)

```powershell
# 设置 PowerShell 执行策略
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
# 下载安装脚本
irm get.scoop.sh -outfile 'install.ps1'
# 执行安装, --ScoopDir 参数指定 Scoop 安装路径
.\install.ps1 -ScoopDir 'C:\Scoop'
```

这么说你可能还是理解不了，那么我们来举个例子好了。正常情况下，你想要允许java，就得有java环境。如果你不知道包管理工具的话，你需要去下载java安装器，安装好了还需要去配置系统环境，非常的麻烦，有了包管理工具的话只需要打开你的shell，输入一行命令就好了

在Macos中
```shell
brew install openjdk
```

Windows
```shell
scoop install openjdk
```

如果你想了解更多，也请自行Google一下。

### 结尾

环境配置堪称“环境科学”，配置环境通常是令人最烦的事情，~~ 被折磨多了也就会配了 ~~这里鼓励大家多动手去配置环境，多多利用搜索引擎去解决问题，你遇到的问题百分之九十九都有解决方案，网络上也有数不清的博客可以参考。

>来自Delusion:在学习初期，如果你不想让乱七八糟的开发环境充斥着你的电脑，可以试试先用虚拟机开发，等到熟练之后再将本地也配上环境也是没问题的。
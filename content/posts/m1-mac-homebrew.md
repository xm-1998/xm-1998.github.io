---
title: M1 Mac安装Homebrew
date: 2021-08-28
author: 夏明
---

本文介绍如何在搭载M1芯片的Mac电脑上快速安装Homebrew，我在自己的M1 MacBook Pro上亲测可行！

## 下载安装脚本

进入Homebrew官网（https://brew.sh/）下载安装脚本到本地。

## 替换国内镜像源

使用编辑器打开Homebrew安装脚本，搜索`HOMEBREW_BREW_DEFAULT_GIT_REMOTE`和`HOMEBREW_CORE_DEFAULT_GIT_REMOTE`，将值替换成与下方相对应的地址：

```
https://mirrors.ustc.edu.cn/brew.git

https://mirrors.ustc.edu.cn/homebrew-core.git
```

## 安装Homebrew

进入bash终端`bash`运行安装脚本`/bin/bash brew_install`，安装完成后退出bash`exit`。

## 添加PASH

在终端打开.zshrc`open ~/.zshrc`，如果没有这个文件就新建一个`touch .zshrc`，添加以下命令：

```
path=('/opt/homebrew/bin' $path)
export PATH
```

最后保存文件，重启终端，输入brew就可以看到Homebrew已经安装成功了！

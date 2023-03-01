---
title: M1 Mac搭建前端开发环境
date: 2021-08-28
author: 夏明
---

本文介绍如何在搭载M1芯片的Mac电脑上搭建Web前端开发环境，我在自己的M1 MacBook Pro上亲测可行！

## 安装nvm

在终端执行以下命令：

```bash
git clone https://gitee.com/mirrors/nvm.git ~/.nvm

cd ~/.nvm

git checkout `git describe --abbrev=0 --tags`
```

### 解决commond not found:nvm

1.进入.nvm文件夹`cd ~/.nvm`

2.查看有没有.bash_profile文件，如果有的话直接打开`open .bash_profile`，如果没有的话先新建 `touch .bash_profile`，新建完成之后打开，粘贴以下代码保存：

```
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"
```

3.编译.bash_profile`source .bash_profile`

4.检查是否可以使用，直接执行`nvm`

### 解决每次关闭终端后，都需要重新编译.bash_profile才能使用nvm

原因：没有将配置添加到.zshrc文件中

1.到这里的时候需要看看我们是否有.zshrc文件，如果有就直接打开`open ~/.zshrc`

```
export NVM_DIR=~/.nvm
[ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh"
```

2.如果没有.zshrc文件，先新建`touch .zshrc`，新建完成之后打开`open -e .zshrc`，粘贴`source ~/.bash_profile`保存，保存完成之后刷新环境`source .zshrc`

## 安装Node.js

使用nvm安装Node.js

```bash
nvm install v14.17.5
```

## 安装VS Code

官网：https://code.visualstudio.com/

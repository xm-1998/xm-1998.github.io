---
title: 前端常用网站及工具
date: 2022-02-22
author: 夏明
---

## 常用网站

### 必知

w3school：https://www.w3school.com.cn/index.html

菜鸟教程：https://www.runoob.com/

Sass官网（CSS预处理器，通过编程的方式来开发CSS）：https://sass-lang.com/

Sass官网（CSS预处理器，通过编程的方式来开发CSS）：https://sass-lang.com/

Less官网（CSS预处理器，通过编程的方式来开发CSS）：http://lesscss.org/

ES6入门（阮一峰大佬的）：http://es6.ruanyifeng.com/

babel（将ES6代码转为ES5代码）：https://babeljs.io/

MDN开发者文档：https://developer.mozilla.org/zh-CN/

NodeJS官网：http://nodejs.cn/

### 三大流行框架

Vue.JS：https://cn.vuejs.org/

Angular：https://www.angular.cn

React：https://react.docschina.org/

### 常用组件库及插件

饿了么element-ui：https://element.eleme.cn/

Ant Design：https://ant.design/components/overview-cn/

Ant Design of Vue：https://www.antdv.com/docs/vue/introduce-cn/

mint-ui：http://mint-ui.github.io/docs/

vant-ui：https://vant-contrib.gitee.io/vant/

iViewUI：https://www.iviewui.com/

阿里图标库：https://www.iconfont.cn/

图表库Echarts：https://www.echartsjs.com/index.html

### 前端打包工具

webpack：https://webpack.js.org/

gulp中文文档：https://www.gulpjs.com.cn/docs/

### 代码托管

github代码托管平台：https://github.com/

git官网：https://git-scm.com/

coding代码托管平台：https://coding.net/

码云代码托管平台：https://gitee.com/

SVN代码托管平台：https://svnbucket.com/

SVN代码托管中心：http://www.svnchina.com/

### 常看

CSDN：https://csdn.net/

思否（问答网站）：https://segmentfault.com/

掘金：https://juejin.cn/frontend

OSCHINA：https://www.oschina.net/

## 常用工具

Sourcetree（GIt可视化工具）：https://www.sourcetreeapp.com/

Snipaste（截图贴图工具）：https://zh.snipaste.com/

Vetur（VSCode插件，VSCode应用商店搜索安装）

ESLint（VSCode插件，VSCode应用商店搜索安装），配置方法如下：

在`settings.json`文件中加入以下代码：

```json
"eslint.validate": [
    "javascript",
    "javascriptreact",
  {
    "language": "html",
    "autoFix": true
  },
  {
    "language": "vue",
    "autoFix": true
  }
],
"eslint.autoFixOnSave": true,
```

vue-devtools，安装方法如下：

1. 运行命令：`npm install vue-devtools`

2. 进入`node_modules/vue-devtools/vender`，打开`manifest.json`，修改`persistent`为`true`，保存

3. 在chrome的扩展程序页面里加载已解压的扩展程序，选择vender文件夹即可

---
title: Hello Hexo
date: 2017-04-01
---
想建一个自己的博客很久了，然而事务杂忙（其实只是在看火影和王座）。拖到现在才来完成今年的小目标。搭建的过程中在网上看了很多很多博客，在这里就不一一列举了。然后自己汇总了一下，就贴在这里，以替换例行的Hello World。
## 安装Hexo与配置
### 前期准备工作
安装``node.js``的环境，包括``nvm``的安装、``node.js``具体版本的安装（其实我是一枚前端渣^_^哈哈哈）
PS:Mac下通过``homebrew``（可以参看我的[``homebrew``安装教程](#)）神器安装``nvm``，再``nvm install node.js``的某版本即可
```  bash
$ alias nvminit_sq='. "$(brew --prefix nvm)/nvm.sh"'
```
### 安装hexo
``` bash
$ npm install -g hexo-cli
```
### 初始化hexo文件夹
先``cd``到为``hexo``准备的文件夹，然后执行：
```  bash
$ hexo init
```

## github准备与操作
在github上创建名为yourname.github.io的repository，这里yourname一定要换成你自己的github的username

### 配置hexo
修改``hexo``目录下的``_config.yml``文件的末尾：
```
deploy:
  type: git
  repository: git@github.com:yourname/yourname.github.io.git
  branch: master
```
同理，yourname换成你的github的username
### 安装git部署工具
在hexo的目录下执行命令：
``` bash
$ npm install hexo-deployer-git --save
```
## 写作与发布
```
$ hexo new "My New Post"
```
更多信息: [写作](https://hexo.io/zh-cn/docs/writing.html)
### 运行服务
```
$ hexo server
```
更多信息: [服务](https://hexo.io/zh-cn/docs/server.html)
### 生成静态文件
```
$ hexo generate
```
更多信息:  [生成](https://hexo.io/zh-cn/docs/generating.html)
### 部署远程服务器
``` bash
$ hexo deploy
```
更多信息:  [部署](https://hexo.io/zh-cn/docs/deployment.html)
至此博客搭建完成，浏览器输入yourname.github.io即可看到个人博客的内容
## 总结
去年离开[59store](www.59store.com)的时候我就定下了几个今年必须拿下的几个小目标，终于可以划掉一个啦啦啦^_^！
参考了很多资料，原来打算用我弱鸡的全栈经验（一个数据后台的开发经验）来部个lamp，后来服务器都准备好了（花了我很多大洋），想多参考别人的bolg再下手干，发现很多技术博客都有自豪的采用WordPress，power by Typecho,hexo强力驱动...云云，Google了下发现了许多托管GitHub的静态博客框架（还有不要买服务器的惊艳到了@……@），比较流行的有Jekyll，Hexo，Simple，Octopress，Pelican以及Lo·gecho等等。最终选定了Hexo来搭建自己的博客，主要原因是Hexo的教程多吧^-^

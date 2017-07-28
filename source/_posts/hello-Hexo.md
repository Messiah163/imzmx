title: Hello Hexo ——Hexo安装与使用
comments: true
date: 2017-04-01 00:00:00
---
## 前期准备工作
``hexo``需要依赖``git``，``node.js``所以第一步需要备好``git``，``node.js``检测是否有依赖环境。
```sh
$ command -v git
$ command -v npm
```
### Git环境安装
### node.js安装
虽然可以[直接安装node.js](https://nodejs.org/en/download/)，但是为了更好的管理node.js以及后期的版本调试，强烈建议不要直接安装。网络上流传着两种node.js版本管理工具，``n``，``nvm``。此处推荐使用``nvm``,具体选择可以[参见淘宝前端团队的文章](http://taobaofed.org/blog/2015/11/17/nvm-or-n/)
#### 安装NVM
参见[NVM官方文档](http://nvm.sh)，先检测是否有``nvm`` ``$ command -v nvm``
如果有curl可以执行
```sh
$ curl -o-https://raw.githubusercontent.com/creationix/nvm/v0.33.2/install.sh | bash
```
或者有Wget执行
```sh
$ wget -qO- https://raw.githubusercontent.com/creationix/nvm/v0.33.2/install.sh | bash
```
执行脚本将clone ``nvm`` 到 `~/.nvm` 并添加资源文件路径到配置文件(`~/.bash_profile`, `~/.zshrc`, `~/.profile`, or `~/.bashrc`)中
```sh
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh" # This loads nvm
```
执行`$ command -v nvm`（安装完成后，重启终端执行校验）

注意：切记不要使用`brew`安装`nvm`

参见[官方文档](https://github.com/creationix/nvm#important-notes)说明 Homebrew installation is not supported. If you have issues with homebrew-installed `nvm`, please `$ brew uninstall` it, and install it using the instructions below, before filing an issue.

#### NVM安装管理node.js
```  bash
$ nvm ls-remote #查看远程node.js版本
$ nvm install v8.1.4 #安装特定版本node.js
$ nvm install v8.2.0
$ nvm install stable #安装稳定版本node.js
$ nvm list #查看nvm安装具体模块
$ nvm use v8.1.4 #切换特定版本node.js
$ nvm current #查看当前版本node.js
```


### 利用npm安装hexo
``` bash
$ npm install -g hexo-cli # -g 或 --global 将在本地全局安装hexo
```
#### 错误排查 
如果是第二次安装`hexo`或者已有本地hexo blog文件，最好是重新安装原有的模块，不然会出现各类的Error如果出现错误也不必紧张,这里博主已经为你踩过了两个常见的坑，欢迎留言交流

1、{ Error: Cannot find module './build/Release/DTraceProviderBindings'...
此类错误出现在OS X给出的[解决方案](https://github.com/hexojs/hexo/issues/1326#issuecomment-113871796)通常是:

```sh
$ npm install hexo --no-optional
```
但是有时候会失效，一般是因为全局安装模块的原因，所以博主的解决方案是
```sh
$ npm uninstall -g hexo-cli #本地全局卸载hexo-cli
```
如果有本地blog项目或者其他已经安装的hexo 下的 node_modules 先全部删除再从新安装
```sh
$ npm install -g hexo-cli --no-optional #本地全局无选项安装hexo模块
$ npm install -g hexo --no-optional  --save #本地全局无选项安装hexo插件模块
```
再次执行`hexo --version`发现问题解决

2、(node:16924) [DEP0061] DeprecationWarning: fs.SyncWriteStream is deprecated.

先查看`$ npm ls | grep hexo-fs` 发现`│ │ ├── hexo-fs@0.1.6 deduped`
可能是版本太低，重新安装`$ npm install hexo-fs --save`
如果没有解决
```
│ │ ├── hexo-fs@0.2.1 deduped
│ ├── hexo-fs@0.1.6 deduped
├─┬ hexo-fs@0.2.1
```
可以发现是某一个模块里面的hexo-fs版本依然太低，博主通过手动替换目录下的hexo-fs低版本解决了问题

3、其他问题参见[Hexo问题解答](https://hexo.io/zh-cn/docs/troubleshooting.html)

## Hexo使用
### 建站
先``cd``到为``hexo``准备的文件夹，然后执行：
```  bash
$ hexo init <folder>
$ cd <folder>
$ npm install #可以不执行全局安装，防止模块冲突报错
```

### 部署
部署前需要在github上创建名为yourname.github.io的repository，这里yourname一定要换成你自己的github的username，并在仓库setting中配置本地ssh的公钥

接着安装git支持模块
```
$ npm install hexo-deployer-git --save
```
然后修改`_config.yml`配置
```
deploy:
  type: git
  repository: git@github.com:yourname/yourname.github.io.git
  branch: master
```

### 写作与发布
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
### 发布到远程服务器
``` bash
$ hexo deploy
```
更多信息:  [部署](https://hexo.io/zh-cn/docs/deployment.html)
至此博客搭建完成，浏览器输入yourname.github.io即可看到个人博客的内容
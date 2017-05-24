title: Apache 调错笔记
author: Messiah
tags:
  - Apache
  - 服务器
categories:
  - 调错笔记
date: 2017-05-24 16:44:00
---
## Apache 报AH00558，AH00072，AH00015错误

#### AH00558
``` bash
$ apachectl configtest
AH00558: httpd: Could not reliably determine the server's fully qualified domain name, using messiah.local. Set the 'ServerName' directive globally to suppress this message
Syntax OK
```
将生效的apache配置文件httpd.conf中的 ServerName 改成可用域名或如下配置
``` bash
ServerName localhost
```
#### AH00072

```
$ apachectl restart
httpd not running, trying to start
(13)Permission denied: AH00072: make_sock: could not bind to address [::]:80
(13)Permission denied: AH00072: make_sock: could not bind to address 0.0.0.0:80
no listening sockets available, shutting down
AH00015: Unable to open logs
```
命令的权限不够,可以通过sudo运行，或者修改Apache的权限。

``` bash
$ sudo apachectl restart
```

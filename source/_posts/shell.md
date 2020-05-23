---
layout: page
title: shell
categories: [工程能力]
tags: [cs]
keywords: 
description: 摘要描述
mathjax: true
---

## curl

[curl](<http://www.codebelief.com/article/2017/05/linux-command-line-curl-usage/>)

不加任何选项使用 curl 时，默认会发送 GET 请求来获取链接内容到标准输出，使用 -d 则默认为发送 POST 请求，-X 可显示地指定发送数据的方式。其他选项如下：

1. -l 只显示 HTTP 头，而不显示文件内容（若要同时显示 HTTP 头和文件内容，使用 -i 选项）;
2. -A 使用自定义 User-Agent 来对网页进行请求；
3. -d 用于指定发送的数据，可用程序内嵌数据-d “somedata”，也可从文件中读取-d “@data.txt”，

## requests

[requests](<https://www.jianshu.com/p/d78982126318>)

`requests.request(method,url,**kwargs)`：

`method`：新建Request对象要使用的HTTP方法，包括：GET，POST，PUT，DELETE等
`url`：新建Request对象的URL链接
`**kwargs`：13个控制访问的可选参数

* params：字典或字节序列，作为参数增加到url中
* data：字典、字节序列、文件，作为Request对象body的内容
* json：JSON格式的数据，作为Request对象body的内容
* headers：字典格式，HTTP请求头，作为Request对象Header的内容
* cookies：字典或CookieJar，Request中的cookie
* files：字典，形式为{filename: fileobject}，用于多文件上传
* auth：Auth 句柄或 (user, pass) 元组
* timeout：等待服务器数据的超时限制，是一个浮点数，或是一个(connect timeout, read timeout) 元组
* allow_redirects：True/False，默认为Ture，重定向开关,为True时表示允许POST/PUT/DELETE方法重定向
* proxies：字典类型，用于将协议映射为代理的URL
* verify：True/False，默认为True，认证SSL证书开关；为True时会验证SSL证书，也可以使用cert参数提供一个CA_BUNDLE路径；为False时，忽略SSL验证
* stream：True/False，默认为True，获取body立即下载开关，为False会立即下载响应头和响应体；为True时会先下载响应头，当Reponse调用content方法时才下载响应体
* cert：为字符串时应是 SSL 客户端证书文件的路径(.pem格式，文件路径包含密钥和证书)，如果是元组，就应该是一个(‘cert’, ‘key’) 二元值对

## shell 中的括号

### ${var}

限定变量名称范围

``` bash
#!/bin/sh
# test.sh
var=test
echo ${var}12
```

效果如下

``` bash
$ ./test.sh
$ var12
```

### $(cmd)

命令替换

``` bash
#!/bin/sh
# test.sh
echo $(ls)
```

运行效果与 `ls` 相同

### {}或()

一串命令的执行

``` bash
$ { echo 1;echo "A";} > tmp
$ cat ./tmp
$ 1
$ A
```

### \${var:-string},\${var:+string},\${var:=string},\${var:?string}

几种特殊的替换结构

#### ${var:-string}
若`var`为空，则结果为`"string"`，否则结果为`$var`。

#### ${var:=string}
若`var`为空，则结果为`"string"`，并将该字符串赋给`var`，否则结果为`$var`。

#### ${var:+string}
若`var`不为空，则结果为`"string"`，否则结果为`$var`。

#### ${var:?string}
若`var`不为空，则结果为`$var`，否则将`"string"`输出到标准错误中，并从脚本退出。

### $((exp))

POSIX标准的扩展计算，只要符合C的运算符都可用在$((exp))，甚至是三目运算符。

### \${var%pattern},\${var%%pattern},\${var#pattern},\${var##pattern}

四种模式匹配替换结构

### []或[[]]

类似test

### ()

在子shell中运行

### {}

{1..30} 就是1-30，或者是/{,s}bin/表示/bin/和/sbin/，ab{c,d,e}表示abc、abd、abe

>[reference](http://www.jb51.net/article/60326.htm)

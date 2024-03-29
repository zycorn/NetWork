﻿# WEB漏洞-必懂知识点

标签（空格分隔）： 网络安全

---

![image_1g5e35qvt1cga1h7fs0q1gu71rm613.png-124.1kB][1]


## 简要说明以上漏洞危害情况
### SQL注入危害
> 1.攻击者未经授权可以访问数据库中的数据，盗取用户的隐私以及个人信息，造成用户的信息泄露。
2.可以对数据库的数据进行增加或删除操作，例如私自添加或删除管理员账号。
3.如果网站目录存在写入权限，可以写入网页木马。攻击者进而可以对网页进行篡改，发布一些 违法信息等。
4.经过提权等步骤，服务器最高权限被攻击者获取。攻击者可以远程控制服务器，安装后门，得 以修改或控制操作系统

### 文件上传危害
> 如果 Web应用程序存在上传漏洞 , 攻击者甚至可以将一个webshell直接上传到服务器上

### XSS危害
> 1.窃取管理员帐号或Cookie，入侵者可以冒充管理员的身份登录后台。使得入侵者具有恶意操纵后台数据的能力，包括读取、更改、添加、删除一些信息。
2.窃取用户的个人信息或者登录帐号，对网站的用户安全产生巨大的威胁。例如冒充用户身份进行各种操作
3.网站挂马。先将恶意攻击代码嵌入到Web应用程序之中。当用户浏览该挂马页面时，用户的计算机会被植入木马
4.发送广告或者垃圾信息。攻击者可以利用XSS漏洞植入广告，或者发送垃圾信息，严重影响到用户的正常使用

### 文件包含危害
> 1.web服务器的文件被外界浏览导致信息泄露
2.脚本被任意执行，可能会篡改网站、执行非法操作、攻击其他网站

### 反序列化危害
> 远程攻击者利用漏洞可在未经任何身份验证的服务器主机上执行任意代码，被攻击者间接控制服务器

### 代码执行危害
> 1.代码执行漏洞造成的原理是由于服务器端没有针对执行函数做过滤，导致在没有指定绝对路径的情况下就执行命令，可能会允许攻击者通过改变 $PATH 或程序执行环境的其他方面来执行一个恶意构造的代码。造成代码执行相关的函数分别是：eval、assert函数
2.暴露服务器信息
3.木马植入
4.敏感文件暴露
5.可能升级为命令执行

### 逻辑漏洞危害
> 1.在提交订单的时候抓取数据包或者直接修改前端代码，然后对订单的金额任意修改。
2.黑客只需要抓取Response数据包便知道验证码是多少或直接绕过
3.有些业务的接口，因为缺少了对用户的登陆凭证的较验或者是验证存在缺陷，导致黑客可以未经授权访问这些敏感信息甚至是越权操作
4.有些关键性的接口因为没有做验证或者其它预防机制，容易遭到枚举攻击
5.Cookie的效验值过于简单。有些web对于cookie的生成过于单一或者简单，导致黑客可以对cookie的效验值进行一个枚举
6.单纯读取内存值数据来当作用户凭证
7.用户修改密码时，邮箱中会收到一个含有auth的链接，在有效期内用户点击链接，即可进入重置密码环节。而大部分网站对于auth的生成都是采用rand()函数，那么这里就存在一个问题了，Windows环境下rand()最大值为32768，所以这个auth的值是可以被枚举的

### 未授权访问危害
> 敏感信息泄漏

### CSRF危害
> csrf(用户请求伪造)
1.以受害者名义发送邮件，发消息，盗取受害者的账号，甚至购买商品，虚拟货币转账，修改受害者的网络配置（比如修改路由器DNS、重置路由器密码）等等
2.个人隐私泄露、机密资料泄露、用户甚至企业的财产安全

### SSRF危害
> ssrf（服务器端请求伪造）
1.可以对外网、服务器所在内网、本地进行端口扫描，获取一些服务的banner 信息
2.攻击运行在内网或本地的应用程序
3.攻击内外网的 web 应用，主要是使用 GET 参数就可以实现的攻击(如：Struts2，sqli)
4.下载内网资源(如：利用file协议读取本地文件等)
5.进行跳板
6.无视cdn
7.利用Redis未授权访问，HTTP CRLF注入实现getshell

### 目录遍历危害
> 攻击者通过访问网站某一目录时，该目录没有默认首页文件或没有正确设置默认首页文件，将会把整个目录结构列出来，将网站结构完全暴露给攻击者； 攻击者可能通过浏览目录结构，访问到某些隐秘文件（如PHPINFO文件、服务器探针文件、网站管理员后台访问地址、数据库连接文件等）

### 文件读取危害
> 1.可以下载服务器的任意文件，包括脚本代码，系统敏感文件
2.可以配合其他漏洞，构成完整攻击链
3.进行代码审计，查找更多的漏洞

### 文件下载危害
> 通过任意文件下载，可以下载服务器的任意文件，web业务的代码，服务器和系统的具体配置信息，也可以下载数据库的配置信息，以及对内网的信息探测等等

### 命令执行危害
> 命令执行，一般都是执行电脑上面的cmd命令，可以通过cmd命令获取目标的敏感信息如（ip地址等）

### XXE危害
> 1.读取任意文件
2.执行系统命令
3.探测内网端口
4.攻击内网网站

## 简要说明以上漏洞等级划分
> 漏洞危害决定漏洞等级：
高危漏洞：SQL注入、文件上传、文件包含、代码执行、未授权访问、命令执行
影响：直接影响到网站权限和数据库权限，能够获取数据或者网站的敏感文件。涉及到数据安全和权限的丢失都为高危漏洞
中危漏洞：反序列化、逻辑安全
低危漏洞：XSS跨站、目录遍历、文件读取
影响：网站的源码，网站部分账号密码

## 简要说明以上漏洞重点内容
> CTF：SQL注入、文件上传、反序列化、代码执行
SRC：漏洞都有可能出现，逻辑安全出现比较多
红蓝对抗：涉及高危漏洞，文件上传、文件包含、代码执行、命令执行

## 简要说明以上漏洞形式问题


  [1]: http://static.zybuluo.com/corn/el1kw9v5bnhxdll0o7ahw2y8/image_1g5e35qvt1cga1h7fs0q1gu71rm613.png
# vulhub漏洞靶场搭建与使用

标签（空格分隔）： 网络安全

---

## 一、安装
### 1.1准备
> 需要先安装一个centos虚拟机
参考 https://www.zybuluo.com/corn/note/2292109
CentOS 7（VMware虚拟机）：搭建环境漏洞环境
 + 网络连接配置：NAT模式
 + IP地址：192.168.79.135
Windows10 （宿主机）：
 + IP地址：192.168.10.22

### 1.2安装Docker
> 参考 https://www.zybuluo.com/corn/note/2292125
查看是否安装成功，存在Client和Server表示安装启动都成功了

### 1.3安装docker- compose
这里使用的是官方安装，不易出现问题·，缺点是有点慢
所以用daocloud下载
以下命令手动修改版本号,例如1.24.1
> sudo curl -L https://get.daocloud.io/docker/compose/releases/download/1.25.1/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose

添加执行权限
> chmod +x /usr/local/bin/docker-compose

检查docker compose版本
> docker-compose version

### 1.4下载vulhub
1.先安装git命令
> yum install -y git

2.下载安装vulhub
> git clone https://github.com/vulhub/vulhub.git

![image_1g3vml55t4qq1v1v1q6h1et01p9r2a.png-28.1kB][1]

## 二.使用
### 2.1启动Docker
> service docker start

![image_1g3vlj5mhlsp17ke38t1f0k14l013.png-992.6kB][2]
查看服务是否启动
> systemctl | grep docker

![image_1g3vlk8b612o4gh4qdn126k1o1c9.png-1000.2kB][3]
### 2.2启动靶场
#### 2.2.1 启动环境
先进入vulhub目录下，选择某个环境，进入对应目录。如httpd注入漏洞，例如我们进入httpd目录下的CVE-2017-15715
> cd vulhub/httpd/CVE-2017-15715

![image_1g3vmtjeo1dh414dppcq1r231sls9.png-28.9kB][4]

### 2.3进入github里找到对应的目录，安装教程进行搭建
![image_1g3vn1linur91ohr1ftq1gkn6t11g.png-144.2kB][5]
### 2.4进入后直接执行如下命令，进行漏洞靶场的编译和运行：
> docker-compose build
docker-compose up -d

### 2.5访问靶机的IP地址的8080端口
![image_1g3vnodl11mmb1s5g3hv16q91udm9.png-3.5kB][6]
![image_1g3vo15bd1m1t1ge1ac1os615hl13.png-40.8kB][7]

### 2.6通过抓包工具进行抓包
> 上传一个名为1.php的文件，之后被拦截

![image_1g400or7n1brt70bfo219ki1lju9.png-147.7kB][8]
![image_1g400pld9fig1lm5vho1hp568dm.png-27.3kB][9]
### 2.7在1.php后面插入一个\x0A（注意，不能是\x0D\x0A，只能是一个\x0A），不再拦截
#### 2.7.1通过HTTP history将POST请求发送给repeater
![image_1g400thrs10q31lg3cek16voa5j13.png-108.5kB][10]
#### 2.7.2打开Hex，在1.php后面插入一个\x0a,然后点击GO
![image_1g4012j771b25dfe1dgm15lnh981g.png-198.3kB][11]
![image_1g4013c21omh1jhb1egmu4q8au1t.png-207.1kB][12]
![image_1g4014f1osdq1ofp155l18fh193m2a.png-201.4kB][13]
> 这个时候，1.php已经没有被拦截了

### 2.8访问刚才上传的/1.php%0a，发现能够成功解析，但这个文件不是php后缀，说明目标存在解析漏洞
![image_1g4017t435aj1pcb1s041fqcf5g2n.png-118.2kB][14]


  [1]: http://static.zybuluo.com/corn/i3ztbkvoyaufbw9dni234w3t/image_1g3vml55t4qq1v1v1q6h1et01p9r2a.png
  [2]: http://static.zybuluo.com/corn/uoojw8ixa48rf2gmtiftv49n/image_1g3vlj5mhlsp17ke38t1f0k14l013.png
  [3]: http://static.zybuluo.com/corn/rbvdlztb1qkj07mjkaaa4l8i/image_1g3vlk8b612o4gh4qdn126k1o1c9.png
  [4]: http://static.zybuluo.com/corn/lfwneg5oua3i0iipegpdrzzx/image_1g3vmtjeo1dh414dppcq1r231sls9.png
  [5]: http://static.zybuluo.com/corn/eopofymny776gh5tmdgunr9v/image_1g3vn1linur91ohr1ftq1gkn6t11g.png
  [6]: http://static.zybuluo.com/corn/dyzh10ywexmnzcvd2m0vqnvr/image_1g3vnodl11mmb1s5g3hv16q91udm9.png
  [7]: http://static.zybuluo.com/corn/nogm23unw3b1gmiicyxez65h/image_1g3vo15bd1m1t1ge1ac1os615hl13.png
  [8]: http://static.zybuluo.com/corn/p7d9wmer3qvplhh2jt0qhufh/image_1g400or7n1brt70bfo219ki1lju9.png
  [9]: http://static.zybuluo.com/corn/dgcstsdfmk42t020g7xc2qvi/image_1g400pld9fig1lm5vho1hp568dm.png
  [10]: http://static.zybuluo.com/corn/nettm2o0m9waw150oef71edo/image_1g400thrs10q31lg3cek16voa5j13.png
  [11]: http://static.zybuluo.com/corn/t1rwcvyj26v3xacqb88cfa2o/image_1g4012j771b25dfe1dgm15lnh981g.png
  [12]: http://static.zybuluo.com/corn/8ig7qnuo91lx1wmlgpvlwtjx/image_1g4013c21omh1jhb1egmu4q8au1t.png
  [13]: http://static.zybuluo.com/corn/1a2zieiltaofse3ri6x7catt/image_1g4014f1osdq1ofp155l18fh193m2a.png
  [14]: http://static.zybuluo.com/corn/xp0jrqfu38um0i4um055mudv/image_1g4017t435aj1pcb1s041fqcf5g2n.png
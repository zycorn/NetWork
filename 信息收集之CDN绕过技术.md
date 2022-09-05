# 信息收集之CDN绕过技术

标签（空格分隔）： 网络安全

---

## 如何判断目标存在CDN服务？
> 利用多节点技术进行请求返回判断,使用超级ping去访问目标网址，如果各个节点都是响应同一ip，说明有CDN服务，反之则没有。

## 目前常见的CDN绕过技术有哪儿些？
> 子域名查询、邮件服务查询、国外地址请求、遗留文件，扫描全网、黑暗引擎搜索特定文件、dns历史记录，以量打量。

## CDN真是IP地址获取后绑定指定地址
> 更改本地HIOSTS解析指向文件

## 子域名解析小技巧
> 在浏览器中输入目标网址域名，加上www和不加www访问出来的内容都是一样的，主机记录中有*号和www两条记录，一般cdn都是设置在www上面，这个时候就是这个网站上加了CDN，是主站地址

## DNS历史记录=第三方接口（接口查询）
> https://get-site-ip.com/  

## 邮件源码测试对比第三方查询（地区分析）
> 通过接收到的邮件查询对方IP地址，如果和第三方查询的结果不一致，需要去查看该网站的公示信息，如下图，该网站备案号是渝，四川重庆地区，那么再去查看邮箱ip和第三方ip，由此就可判断出邮箱ip是真实ip

![image_1gc5mvl9b12chj2lc2u1luhdca9.png-16.7kB][1]
![image_1gc5n0auv1ine1kemb1m1v7e56rm.png-11.3kB][2]
![image_1gc5n2lviit21t8oesc8cm10mm13.png-11.5kB][3]
![image_1gc5n3n837fcq2qun75fn6vi1g.png-9.5kB][4]
![image_1gc5n40nm1lgf171fts317dgk11t.png-5.2kB][5]

## 黑暗引擎(shodan搜指定hash文件)
> 通过Python脚本获取ico文件的hash值，再去黑暗引擎进行搜索改hash值，即可获取目标网站的ip地址


## 扫全网
> funckcdn,w8fuckcdn,zmap


  [1]: http://static.zybuluo.com/corn/7ivd6kkzabn2fx7oc71yy1do/image_1gc5mvl9b12chj2lc2u1luhdca9.png
  [2]: http://static.zybuluo.com/corn/0ovjsfah0mlq8rdb3hlzv748/image_1gc5n0auv1ine1kemb1m1v7e56rm.png
  [3]: http://static.zybuluo.com/corn/fyliax9kqym7v61e9r6lstns/image_1gc5n2lviit21t8oesc8cm10mm13.png
  [4]: http://static.zybuluo.com/corn/lzreic0n01x6t9fv9mb69nc7/image_1gc5n3n837fcq2qun75fn6vi1g.png
  [5]: http://static.zybuluo.com/corn/8ir9gd8ppxf57opkn0j216cu/image_1gc5n40nm1lgf171fts317dgk11t.png
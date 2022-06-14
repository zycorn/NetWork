# WEB漏洞-SQL注入之简易sql注入

标签（空格分隔）： SQL注入

---

## SQL注入
> SQL注入就是一种通过操作输入来修改后台SQL语句达到代码执行进行攻击目的的技术

## sql注入产生原因
> 接收数据 拼接数据 数据库执行 结果展示— 四个步骤，过程中处理不当就可能会存在注入漏洞
sql注入漏洞，取决于过滤严谨与否，过滤严谨，基本不可能存在sql注入漏洞，反之，就可能存在！

## SQL注入的危害
> 1.危害数据库里的数据
2.直接危害网站的权限

## SQL 注入知识结构
![image_1g5h21o1dbro176v1dae1b8p1bod9.png-108.9kB][1]

## mysql数据库注入
![image_1g5h23gondda1fig1d9316r4159qm.png-89.6kB][2]

## mysql数据库
> 数据库A=网站A=数据库用户A
表名——> 列名 ——> 数据(目标)
数据库B=网站B=数据库用户B
…
数据库C=网站C=数据库用户C
…

## 如何判定是否存在注入点？
> 老办法：
and 1=1 页面正常
and 1=2 页面异常
原理：
SELECT * FROM users WHERE id=1 LIMIT 0,1
SELECT * FROM users WHERE id=1 and 1=1 LIMIT 0,1 正常
SELECT * FROM users WHERE id=1 and 1=2 LIMIT 0,1 错误
逻辑运算（与 或 非）
真 且 真 = 真
真 且 假 = 假
真 或 假 = 真
SELECT * FROM users WHERE id=1 真
and（且） 1=1 真 =真
and（且） 1=2 假 =假
不要局限于此
SELECT * FROM users WHERE id=1xxxx(随意、怎么舒服怎么来！) LIMIT 0,1
随意输入内容后
对网页有影响说明带入数据库进行查询 有注入点。
对网页没有影响说明没有带入数据库查询
出现404（或者其他、如：跳转主页）说明对输入进行检测 基本没有sql漏洞

## 猜测列名数量（字段数）
> order by x(数字-不断尝试）
正常值 网页正常显示
错误值 错误网页报错

## 信息收集：
> 数据库版本：version（）
数据库名字：database（）
数据库用户：user（）
操作系统： @@version_compile_os

## 视频中出现的题目
> 1.可能存在注入的编号选项有哪几个？
1-www.xiaodi8.com/index.php?id=8
2-www.xiaodi8.com/?id=10
3-www.xiaodi8.com/?id=10&x=1
4-www.xiaodi8.com/index.php(post注入)
答案：1234
2.参数有x注入，以下哪个注入测试正确
A.www.xiaodi8.com/new/php?y=1 and 1=1&x=2
B.www.xiaodi8.com/new/php?y=1&x=2 and 1=1
C.www.xiaodi8.com/new/php?y=1 and 1=1 & x=2 and 1=1
D.www.xiaodi8.com/new/php?xx=1 and 1=1&xxx=2 and 1=1
答案：BC



  [1]: http://static.zybuluo.com/corn/s8wz3lkfaf9edqq5ygkyve1k/image_1g5h21o1dbro176v1dae1b8p1bod9.png
  [2]: http://static.zybuluo.com/corn/cqn7yqbytwks6ht85u0e9y9q/image_1g5h23gondda1fig1d9316r4159qm.png
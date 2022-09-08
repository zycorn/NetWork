# SQL注入之查询方式及报错盲注

标签（空格分隔）： SQL注入

---

当进行SQL注入时，有很多注入会出现无回显的情况，其中不回显的原因可能是SQL语句查询方式的问题导致，这个时候我们需要用到相关的报错或者盲注进行后续操作，同时作为手工注入时，提前了解或预知其SQL语句大概写法也能更好的选择对应的注入语句。


----------

>  select 查询数据
    在网站应用中进行数据显示查询操作
    例：select * from news where id = $id
    
> insert 插入数据
在网站应用中进行用户注册添加等操作
例：insert into news(id,url,text) values(2,'x,'$t)

> delete 删除数据
后台管理界面删除文章删除用户等操作
例：delete from news where id = $id

> uodate 更新数据
会员或后台中心数据同步或缓存等操作
例：update user set pwd='$p' where id = 2 and username='admin'

> order by 排序数据
一般结合表名或者列名进行数据排序操作
例：select * from news order by $id

> 例：select id,nanme,price from news order by $order

## SQL注入报错盲注
> 盲注就是在注入过程中，获取的数据不能回显到前端页面。此时，我们需要利用一些方法进行判断或者尝试，这个过程称之为盲注。我们可以知道盲注分为以下三类：

> 记忆布尔的SQL盲注-逻辑判断（次之）
regexp,like,ascii,left,ord,mid

> 基于时间的SQL盲注-延时判断（最后）
if,sleep

> 基于报错的SQL盲注-报错回显(优先)
floor,uodatexml,extractvalue
https://www.jianshu.com/p/bc35f8dd4f7c

> 参考：
like 'ro%'                          #判断ro或ro...是否成立
regexp '^xiaodi[a-z]'               # 匹配xiaodi及xiaodi...等
if(条件，5,0)                       #条件成立返回5， 反之返回0
sleep(5)                            #SQL语句延时执行5秒
mid(a,b,c)                          #从位置b开始，截取a字符串的c位
substr(a,b,c)                       #从b未知开始，截取字符串a的c长度
left(database(),1),database()       #left(a,b)从左侧截取a的前b位
length(databases())=8               #判断数据库database()名的长度
ord=ascii ascii(x)=97               #判断x的ascii码是否等于97


    




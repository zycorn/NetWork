# sql注入之MySQL注入

标签（空格分隔）： sql注入

---

# 高权限注入及低权限注入
## 跨库查询机器应用思路
> information_schena表特性，记录库名，表名，列名对应表

> 获取所有数据库名
union select 1,group_concat(schema_name),3 from information_schema.schemata


## 文件读写操作（MySQL）
> load_file(文件路径):读取函数
into outfile + ‘路径’或 into dumpfile + ‘路径’ : 文件写入导出

> 路径获取的常见方法：
报错显示，遗留文件，漏洞报错，平台配置文件，爆破等

## 自带防御
> PHP魔术引号或者addslashes()，会对路径进行加上反斜杠，可以使用16进制编码和宽字节绕过

## 内置函数：int is_int
## 自定义关键字：select str_replace
## WAF防护软件：安全狗，宝塔等
## 绕过WAF
> 更改提交方法、大小写混合、解密编码类、注释符混用、等价函数替换、特殊符号混用、借助数据库特性、HTTP参数污染、垃圾数据溢出

## 低版本注入配合读取或暴力
> 字典或读取  sqlmap
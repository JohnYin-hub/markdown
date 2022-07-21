### Hive sql正则查询

```sql
set hive.support.quoted.identifiers=none; #配置hive 一般不需要使用
SELECT ‘login.*’ from new_raw_log
where login_status != "failed"LIMIT 100;
```

### 数据库连接

协议：JDBC

数据库源：driver、url、username、password

执行语句：select、insert、update、deletw。。。。

操作：Connection、PrepareStatement、Result

mybatis 读取MySQL的三部曲，数据库源+执行语句+操作

源码三部曲：宏观、微观、图解




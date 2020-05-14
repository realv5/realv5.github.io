### mysql多数据下查询注意点
1. 要命中索引
2. 在使用查询出来的列在其他地方没有使用到的情况下应该避免使用集合函数
3. 尽量只返回所需要的列
4. 尽量需要使用分页查询

### mysql 安装 rpm 
``` shll
rpm -ivh Mysql-server-XXX.rpm
rpm -ivh Mysql-client-XXX.rpm
```
### mysql 设置用户密码
- /usr/bin/mysqladmin -u root password 123456

### 常用语句
``` sql
    -- 统计数据库中表的行数
    use information_schema;
    select table_name,table_rows from tables where TABLE_SCHEMA = 'talbe_name' order by table_rows desc; 
```

### mysql命令大全
[Mysql命令大全]https://www.cnblogs.com/zhangzhu/p/3172486.html



### mysql高级
[MySQL高级 之 explain执行计划详解](https://blog.csdn.net/wuseyukui/article/details/71512793)

[MySQL大表优化方案](https://segmentfault.com/a/1190000006158186)

[MYSQL-索引](https://segmentfault.com/a/1190000003072424)


[查询过程](https://mp.weixin.qq.com/s?__biz=MzI4MDYwMDc3MQ==&mid=2247486387&idx=1&sn=9270e6f72b0e73ed5a31df3d7f591e17&chksm=ebb7421fdcc0cb097989b4614090a589f5f257c82ee388d366333ba8b54ef673d28ec08b9a03&mpshare=1&scene=22&srcid=#rd)


### mysql 高级用法
```mysql
# CONCAT 函数用于将两个字符串连接为一个字符串
SELECT CONCAT(businfo_name,businfo_creditCode) FROM tb_businfo LIMIT 0,10;
# CONCAT_WS 函数用于将两个字符串连接为一个字符串,第一个参数是其它参数的分隔符
# mysql CONCAT_WS()不会忽略任何空字符串。 (然而会忽略所有的 NULL）
SELECT CONCAT_WS(',',businfo_name,businfo_creditCode) FROM tb_businfo LIMIT 0,10;

```

mysql 高级用法

### 时间日期计算
[年月日计算](https://www.cnblogs.com/shuilangyizu/p/8805384.html)

### Linux下默认是区分大小写修改
用 root 登录，修改 /etc/my.cnf （注意：以实际 my.cnf 配置文件路径为准）
在 [mysqld] 节点下，加入一行： lower_case_table_names=1

用 `show variables like '%case%';` 查看
### 逻辑架构分层
1. 第一：连接、线程处理、授权认证、安全等等
2. 第二：核心服务功能层，包含查询解析，分析，优化，缓存以及内置函数等
3. 第三：存储引擎，负责mysql中数据的存储与提取

### 查询优化
- 使用`explan` 它可以对 `SELECT` 语句进行分析， 例如：`explan select * from table where id <100;`
- 优化器不关心表使用什么存储引擎，但存储引擎对于优化查询有影响。
- 对于`select`语句在查询之前会进行缓存，如果检测到有缓存则直接输出缓存结果，服务器不必在执行查询解析、优化和执行整个过程。

### 事务
- 事务就是一组原子性的sql查询，或者说是一个独立的工作单元。
- `ACID` 表示原子性（atomicity）、一致性（consistency）、隔离性（isolation）和持久性（durability）。一个良好的事务处理系统，必须具备这些标准特征。

### mycat
数据库负载增大的处理方法


- 字段设计：
- 状态字段要看它是不是互斥；互斥就可以在同一字段上标注不同状态，不互斥就要分开字段显示；

`OSS` 阿里云对象存储
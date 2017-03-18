#### Day11

> 1,增删改
```
1,数据库设计规范：
        1，原子xing性
        2，唯一性
        3，独立性
2，数据库操作：
        insert into table_name ([a],[b]) values (a1,a2);
        replace into table_name ([a],[b]) values (a1,a2);
        insert  into  table_name  set  key1=value1，key2=value2；
        insert into table_name (key1,key2) select key_other1,key_otber2 from  table_name2
3, 删除数据
    delete from table_name where [condition] order by key1 desc limit start range;
4, 修改数据
    update table_name set key1=value1,key2=value2 where [condition] order by `id` desc;
```
> 2 ,连接表

```
    1，基本形式
        table_name1 [action] join table_name2 [on condition]
        table_name1 [action1] join table_name2 [confition] [action2] join table_name3
    2, select id name from table_name where price > (select 5000)
    3,select  id  from  table_name  where  name  like ‘%zhangshan%’;
    4,select *from table_name1 union select *from table_name2;
```
3,权限管理
```
授予权限：
    grant  权限列表  on  某库．某个对象  to  ‘用户名’@’允许登录的位置’  【identified  by  ‘密码’】；
    eg:
        grant select, insert, update, delete on testdb.* to common_user@'%'
剥夺权限：
    revoke  权限列表  on  某库．某个对象  from  ‘用户名’@’允许登录的位置’
    其含义，跟grant中完全一样；
```
4,事务：
```
• 原子性：一个事务中的所有语句，应该做到：要么全做，要么一个都不做；
• 一致性：让数据保持逻辑上的“合理性”，比如：一个商品出库时，既要让商品库中的该商品数量减1，又要让对应用户的购物车中的该商品加1；
• 隔离性：如果多个事务同时并发执行，但每个事务就像各自独立执行一样。
• 持久性：一个事务执行成功，则对数据来说应该是一个明确的硬盘数据更改（而不仅仅是内存中的变化）。

1，开启一个事务：
    start  transaction；​//也可以写成：begin；
2，执行多条增删改语句；​//也就是相当于希望这多条语句要作为一个“不可分割”的整体去执行的任务
3，判断这些语句执行的结果情况，并进行提交或回滚：
    if(  没有出错 ）{
    commit；​//提交事务；此时就是一次性完成；
    }
    else{
    rollback；​//回滚事务；此时就是全部撤销；
    }

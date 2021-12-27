## 常用sql语句

#### 修改表某一列所有值

```sql
UPDATE sunon.tb_app_user SET active = '1';

如果报错You are using safe update mode and you tried to update a table without a...

原因：mysql在执行删除更新语句时报这种错误，是因为在mysql在safe-updates模式中，如果你where后跟的条件不是主键id，那么就会出现这种错误。

解决办法：在执行update语句前先执行
SET SQL_SAFE_UPDATES = 0;
```


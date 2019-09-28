SQL语言分为五大类：

- DDL(数据定义语言) - Create、Alter、Drop 这些语句自动提交，无需用Commit提交。
- DQL(数据查询语言) - Select 查询语句不存在提交问题。
- DML(数据操纵语言) - Insert、Update、Delete 这些语句需要Commit才能提交。
- DTL(事务控制语言) - Commit、Rollback 事务提交与回滚语句。
- DCL(数据控制语言) - Grant、Revoke 授予权限与回收权限语句。
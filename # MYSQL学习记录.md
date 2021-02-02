# MYSQL学习记录
## 一、用户
1、创建用户
```
create user 'XXX' identified by '********';
```
2、修改权限（用root赋予所有权限）
```
grant all privileges on *.* to 'XXX';
```

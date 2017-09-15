# Syllabus

1. Python3使用PyMySQL操作Mysql

---

## Q1. 在命令行内直接输入mysql会出现
> command not found:mysql

A: 未加入到环境变量中，需要在用户根目录下。 

1.输入
```
vi .bash\_profile
```

2.在里面加入:
```
export PATH = ‘usr/local/mysql/bin:PATH’
```
后保存退出

3.命令行输入

> \# source ./bash\_porfile
重新载入配置文件即可。

## T2. 首次进入Mysql需要重置密码
A: 
> \# mysql -u root -p
输入安装过程中的随机密码，验证通过需要先更新密码才能进行其他操作：
> mysql> SET PASSWORD = PASSWORD('123456'); 


## T3. 手动更新密码
> mysql> UPDATE mysql.user SET authentication_string=PASSWORD(’新密码’) WHERE User=’root’;
> mysql> FLUSH PRIVILEGES;

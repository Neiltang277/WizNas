## centos7 上安装mysql5.7后登录报错ERROR 1045 (28000): Access denied for user 'root'@'localhost' (using password:yes)

1，停止mysql服务
systemctl stop mysqld.service

2，修改配置文件无密码登录
vi /etc/my.cnf  

在最尾部加上
skip-grant-tables  

3，启动mysql
systemctl start mysqld.service  

4，登录musql
mysql -u root  
此处注意不要加-p

5,修改密码，mysql5.7用此语法
use mysql ;  
update mysql.user set authentication_string=password('123456') where user='root' ;  

6,回到第二步骤去掉加上的
skip-grant-tables  

保存 重启mysql就ok了

---

其实默认安装完了mysql后或在日志中生成一个默认的密码 /var/log/mysqld.log 中
拿到默认密码后登录mysql  进行密码重新设置

set passwprd=password('you password')； 

如果密码级别与默认的级别要求不符时候会报
Your password does not satisfy the current policy requirements  

此时需要修改级别与最小的默认密码位数
set global validate_password_policy=0;  
set global validate_password_length=4;  

然后在进行设置密码就好了

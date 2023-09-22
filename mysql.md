## CentOS7安装MySQL（完整版）

步骤一：首先下载mysql的yum源配置
```
wget http://dev.mysql.com/get/mysql57-community-release-el7-11.noarch.rpm
```
步骤二：安装mysql的yum源
```
yum -y install mysql57-community-release-el7-11.noarch.rpm
```
步骤三：yum方式安装mysq
```
yum -y install mysql-server  --nogpgcheck
--nogpgcheck  (不校验数字签名)
```
步骤四：启动mysql
1.使用systemctl命令启动mysql服务
```
systemctl start mysqld.service
```
查看mysql服务状态
```
systemctl status mysqld.service
```
停止mysql服务
```
systemctl stop mysqld.service
```
重启mysql服务
```
systemctl stop mysqld.service
```
2、命令行进入mysql
```
mysql -u username -p
```
接下来要你输入密码，初始密码存在/var/log/mysqld.log文件里
3、修改mysql密码
首选修改密码验证强度等级为LOW
```
set global validate_password_policy=LOW;
```
否则会出现报错set global validate_password_policy=LOW;
```
ALTER USER USER() IDENTIFIED BY '123456abc';
```
退出mysql
```
quit
```
参考：[CentOS7安装MySQL（完整版）](https://blog.csdn.net/m0_46608037/article/details/123019925)

注意：
如果想使用navicat从外部能够访问的话，需要进行授权，把上面链接中的授权方法

```
grant all privileges on *.* to 'root'@'192.168.0.1' identified by 'password' with grant option;
```
改为
```
grant all privileges on *.* to 'root'@'%' identified by 'password' with grant option;
```
如果还不能连上，需要添加安全组
参考：[使用Navicat连接阿里云服务器中的Mysql数据库](https://blog.csdn.net/kaifaxiaoliu/article/details/80403736)

## php报错Headers and client library minor version mismatch

这是由于在安装mysqli模块时，使用的API library版本与API header版本不一致所致。

解决办法
```
yum remove php-mysql
yum install php-mysql
```
重启apache
```
systemctl restart httpd 或 service httpd restart
```

## 实用mysql语句
in,group by,having筛选多类同名商标
```
SELECT mark_name,COUNT(mark_name) FROM mark_info WHERE mark_category IN (3,10,35) GROUP BY mark_name HAVING COUNT(mark_name) > 2;
```
regexp 同一字段like多个值
```
select * from domain_info where is_onsale = 'sale' and domain_name regexp 'lc.com.cn|kj.com.cn|qc.com.cn'
```

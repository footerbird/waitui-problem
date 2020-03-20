## CentOS7安装MySQL（完整版）

参考：[CentOS7安装MySQL（完整版）](https://blog.csdn.net/qq_36582604/article/details/80526287)

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
SELECT mark_name,COUNT(mark_name) FROM mark_info WHERE mark_category  IN (3,10,35) GROUP BY mark_name HAVING COUNT(mark_name) > 2;
```
regexp 同一字段like多个值
```
select * from domain_info where is_onsale = 'sale' and domain_name regexp 'lc.com.cn|kj.com.cn|qc.com.cn'
```

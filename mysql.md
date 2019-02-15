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

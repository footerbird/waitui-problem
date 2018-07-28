## 一、服务器环境生成图片报错Call to undefined function imagecreate()
原因：这是服务器下没有安装gd库所导致的。
检测有没有安装gd库

1、webshell下命令
```
php -i|grep -i --color gd 或 php -m;
```
2、php查询
```
echo phpinfo()
```

默认CentOS服务器装好后运行的网站并不支持GD库，网上有很多教程非常复杂的讲述了一些安装GD库的方法。其实完全不必如此复杂。

由于CentOS将支持GD库的PHP作为另外一个版本的PHP来发布，如果需要服务器支持GD库，只需要直接安装带GD库的php版本即可。

下面是最简便的安装GD库的方法：

具体操作只有2个命令如下：

运行在线安装带GD库的PHP的命令：
```
yum -y install php-gd
```
重新启动apachce服务以使安装后的GD库生效
```
service httpd restart
```

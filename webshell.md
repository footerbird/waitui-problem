## 一、查看linux下的php环境
```
httpd -v
php -v
```
httpd就是apache的目录

## 二、在linux环境下安装apache和php和php扩展
```
yum -y install httpd
yum -y install php
yum -y install php-gd
yum -y install php-mysql
```
httpd安装完成以后在/etc/文件夹下会出现httpd目录，里面是apache的配置信息

在/var/文件夹下会出现www文件夹，里面放置网站项目，默认www下有html空文件夹，可以在html文件夹下放入index.html替换掉默认网页

安装完成后查看apache状态
```
service httpd status
```

这里php-gd是安装图形库，不然php无法创建图片

php-mysql用来连接mysql数据库

## 三、服务器环境生成图片报错Call to undefined function imagecreate()
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
## 四、配置虚拟站点

在/www/文件夹下分别建三个站点的文件目录doc1,doc2,doc3，然后在/etc/httpd/conf/下添加httpd-vhosts.conf文件，文件内容为
```
<VirtualHost *:80>
    DocumentRoot "/var/www/doc1"
    ServerName www.doc1.com
</VirtualHost>
<VirtualHost *:80>
    DocumentRoot "/var/www/doc2"
    ServerName www.doc2.com
</VirtualHost>
<VirtualHost *:80>
    DocumentRoot "/var/www/doc3"
    ServerName www.doc3.com
</VirtualHost>
```
然后找到/etc/httpd/conf/httpd.conf文件，在最底部加入
```
Include /etc/httpd/conf/httpd-vhosts.conf
```
保存完成后，最后重启apache就可以了


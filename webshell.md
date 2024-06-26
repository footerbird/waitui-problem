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
yum -y install php-zip
yum -y install php-mysql
yum -y install php-redis
yum -y install php-bcmath
```
httpd安装完成以后在/etc/文件夹下会出现httpd目录，里面是apache的配置信息

在/var/文件夹下会出现www文件夹，里面放置网站项目，默认www下有html空文件夹，可以在html文件夹下放入index.html替换掉默认网页

安装完成后查看apache状态
```
service httpd status
```

这里php-gd是安装图形库，不然php无法创建图片

php-mysql用来连接mysql数据库（注意，服务器上的database.php只能连数据库的内网IP）


### （解决报错:Call to undefined function mb_detect_encoding()）

```
yum -y install php-mbstring
yum -y install php-xml
```

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

## 五、路由重写index.php
1、httpd.conf配置文件中加载了mod_rewrite.so模块，AllowOverride None 将None改为 All

2、添加.htaccess文件放到入口文件的同级目录下

## 六、在linux环境下安装mcrypt扩展

首先判断有没有按照mcrypt
```
yum list installed|grep mcrypt
```
如果没有的话

```
yum install libmcrypt libmcrypt-devel mcrypt mhash
```
再按照php-mcrypt

```
yum install php-mcrypt
```
最后重启一下apache

## 七、 linux，centos下php版本升级

参考链接：[https://blog.csdn.net/wuhounuanyangzhao/article/details/79709077](https://blog.csdn.net/wuhounuanyangzhao/article/details/79709077)

## Linux 上传下载文件

```
scp /home/vie/app-phone2.png root@112.17.38.145:/opt/htdocs/yumi.com/htdocs/yumi/m/images/topic
```
上传下载文件夹,-r： 递归复制整个目录。
```
scp -r application/ root@218.205.113.173:/home/htdocs/wencode
```
ssh登录远程服务器
```
ssh vie@112.17.38.136 -p 10022
```

## 在MAC安装brew
```
/bin/zsh -c "$(curl -fsSL https://gitee.com/cunkai/HomebrewCN/raw/master/Homebrew.sh)"
```
## linux如何查看文件夹占用磁盘空间
```
du -h -d 1
```
查看当前目录下面所有文件夹所占的空间

## git寻找历史中的大文件
```
git rev-list --objects --all | grep "$(git verify-pack -v .git/objects/pack/*.idx | sort -k 3 -n | tail -5 | awk '{print$1}')"
```
地址 https://www.dazhuanlan.com/2020/02/02/5e36f1a8991da/

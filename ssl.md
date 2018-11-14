## 一、安装ssl模块(httpd默认不带有ssl模块)
```
yum -y install mod_ssl
```
安装完成后在/etc/httpd/conf.d/目录下会生成ssl.conf文件

## 二、将下载的ssl证书上传到服务器的相关目录（我的证书是在腾讯云的ssl证书管理界面下载的）

上传后三个文件分别对应下面三个地址
```
/etc/pki/tls/certs/1_root_bundle.crt
/etc/pki/tls/certs/2_waitui.com.crt
/etc/pki/tls/private/3_waitui.com.key
```

## 三、配置ssl.conf文件

找到 SSLCertificateFile /etc/pki/tls/ 关键词，并将配置内容替换成我们申请的证书
```
SSLCertificateFile /etc/pki/tls/certs/2_waitui.com.crt
SSLCertificateKeyFile /etc/pki/tls/private/3_waitui.com.key
SSLCertificateChainFile /etc/pki/tls/certs/1_root_bundle.crt
```
把ssl.conf中的服务器名称指向域名监听443端口，这样就可以https访问了

你的域名xxx.xxx.xx.com：443即可。并去掉前面的“#”

保存完成后，最后重启apache就可以了

参考：[https://jingyan.baidu.com/article/adc815138136e8f722bf7353.html](https://jingyan.baidu.com/article/adc815138136e8f722bf7353.html)

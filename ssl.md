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

## 三、配置ssl.conf文件(/etc/httpd/conf.d/ssl.conf)

找到 SSLCertificateFile /etc/pki/tls/ 关键词，并将配置内容替换成我们申请的证书
```
SSLCertificateFile /etc/pki/tls/certs/2_waitui.com.crt
SSLCertificateKeyFile /etc/pki/tls/private/3_waitui.com.key
SSLCACertificateFile /etc/pki/tls/certs/1_root_bundle.crt
```
把ssl.conf中的服务器名称指向域名监听443端口，这样就可以https访问了

你的域名xxx.xxx.xx.com：443即可。并去掉前面的“#”

保存完成后，最后重启apache就可以了

参考：[https://jingyan.baidu.com/article/adc815138136e8f722bf7353.html](https://jingyan.baidu.com/article/adc815138136e8f722bf7353.html)


## 四、茶酒网nginx配置ssl证书

```
server {
  listen       443;
  server_name  test.api.shop.chajiu.cn;

  ssl on;
  ssl_certificate /opt/ssl/1_test.api.shop.chajiu.cn_bundle.crt;
  ssl_certificate_key /opt/ssl/2_test.api.shop.chajiu.cn.key; 
  ssl_session_timeout 1d;
  ssl_session_cache shared:SSL:50m;
  ssl_session_tickets off;
  ssl_protocols TLSv1.2;
  ssl_ciphers 'ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-CHACHA20-POLY1305:ECDHE-RSA-CHACHA20-POLY1305:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES128-SHA256:ECDHE-RSA-AES128-SHA256';
  ssl_prefer_server_ciphers on;
  add_header Strict-Transport-Security max-age=15768000;
  ssl_stapling on;
  ssl_stapling_verify on;

  #允许上传视频最大为10M
  client_max_body_size 10M;
  location /base {
    rewrite /base/(.*) /$1 break;
    rewrite /base /$1 break;
    proxy_pass   http://172.21.0.8:7000;             
    #proxy_set_header Host \$host:\$server_port;
    #proxy_pass_header User-Agent;     
  }
  location /buyer {
    rewrite /buyer/(.*) /$1 break;
    rewrite /buyer /$1 break;
    proxy_pass   http://172.21.0.8:7002;
    #proxy_set_header Host \$host:\$server_port;
    #proxy_pass_header User-Agent;
  }
}
```

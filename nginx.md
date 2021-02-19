## 查看nginx相关文件路径

```
nginx -V

fengxu@FengdeMBP ~ % nginx -V
nginx version: nginx/1.17.10
built by clang 11.0.3 (clang-1103.0.32.29)
built with OpenSSL 1.1.1f  31 Mar 2020 (running with OpenSSL 1.1.1g  21 Apr 2020)
TLS SNI support enabled
configure arguments: --prefix=/usr/local/Cellar/nginx/1.17.10 --sbin-path=/usr/local/Cellar/nginx/1.17.10/bin/nginx --with-cc-opt='-I/usr/local/opt/pcre/include -I/usr/local/opt/openssl@1.1/include' --with-ld-opt='-L/usr/local/opt/pcre/lib -L/usr/local/opt/openssl@1.1/lib' --conf-path=/usr/local/etc/nginx/nginx.conf --pid-path=/usr/local/var/run/nginx.pid --lock-path=/usr/local/var/run/nginx.lock --http-client-body-temp-path=/usr/local/var/run/nginx/client_body_temp --http-proxy-temp-path=/usr/local/var/run/nginx/proxy_temp --http-fastcgi-temp-path=/usr/local/var/run/nginx/fastcgi_temp --http-uwsgi-temp-path=/usr/local/var/run/nginx/uwsgi_temp --http-scgi-temp-path=/usr/local/var/run/nginx/scgi_temp --http-log-path=/usr/local/var/log/nginx/access.log --error-log-path=/usr/local/var/log/nginx/error.log --with-compat --with-debug --with-http_addition_module --with-http_auth_request_module --with-http_dav_module --with-http_degradation_module --with-http_flv_module --with-http_gunzip_module --with-http_gzip_static_module --with-http_mp4_module --with-http_random_index_module --with-http_realip_module --with-http_secure_link_module --with-http_slice_module --with-http_ssl_module --with-http_stub_status_module --with-http_sub_module --with-http_v2_module --with-ipv6 --with-mail --with-mail_ssl_module --with-pcre --with-pcre-jit --with-stream --with-stream_realip_module --with-stream_ssl_module --with-stream_ssl_preread_module
```

## net::ERR_CONTENT_LENGTH_MISMATCH 200 (OK)解决方法

nginx使用域名代理vue项目的时候会出现接口数据请求不到的问题（用localhost+端口号访问能请求到数据），

查看nginx 错误日记 tail -f nginx/logs/error.log，显示 nginx/proxy_temp/ 目录 无权限。

这里比较偷懒的办法，修改目录数据权限

```
chmod -R 777 nginx/proxy_temp/
```

## 解决：NET::ERR_INCOMPLETE_CHUNKED_ENCODING 200 (OK)

常见的原因有如下几种情况：

### 1、nginx的缓冲区（Proxy Buffer）设置较小

修改配置如下：

```
proxy_buffer_size 1024k;
proxy_buffers 16 1024k;
proxy_busy_buffers_size 2048k;
proxy_temp_file_write_size 2048k;
```

### 2、nginx的临时目录（/proxy_temp）过大或没有权限写入缓存文件

当代理文件大小超过配置的proxy_temp_file_write_size值时，nginx会将文件写入到临时目录下（默认为/proxy_temp）。

如果nginx中/proxy_temp过大或者没有写权限，缓存文件就写不进去了。

·直接删除Nginx缓存文件；

```
rm -rf  /usr/local/nginx/proxy_temp
```

·设置Nginx的缓存过期时间；

·调整/proxy_temp权限为配置nginx的那个用户；

```
chown -R www:www /usr/local/nginx/proxy_temp
```

### 3、磁盘空间不够

删掉磁盘一些日志 文件，释放下空间。

参考：[https://blog.csdn.net/willingtolove/article/details/103372199](https://blog.csdn.net/willingtolove/article/details/103372199)

## mac上启动nginx遇到80端口被占用的解决方法

今天启动nginx的时候，发现80端口被占用，用ps -ef | grep nginx和lsof -i:80都找不到，后来上网搜索后发现是apache的问题，是因为系统自带的apache启动了所以占用了ngxin80端口，解决方案是执行下面的代码。

```
sudo apachectl stop
```

然后执行

```
sudo nginx
```

解决

## nginx配置（conf/nginx.conf）

nginx监听3000端口

```
server {
		listen       80;
		server_name  你的域名;

		#后台服务配置，配置了这个location便可以通过http://域名/jeecg-boot/xxxx 访问		
		location ^~ /jeecg-boot {
			proxy_pass              http://127.0.0.1:8080/jeecg-boot/;
			proxy_set_header        Host 127.0.0.1;
			proxy_set_header        X-Real-IP $remote_addr;
			proxy_set_header        X-Forwarded-For $proxy_add_x_forwarded_for;
		}
		#解决Router(mode: 'history')模式下，刷新路由地址不能找到页面的问题
		location / {
			root   html;
			index  index.html index.htm;
			if (!-e $request_filename) {
				rewrite ^(.*)$ /index.html?s=$1 last;
				break;
			}
		}
	}
```

## nginx 开启压缩，提高首页访问效率

nginx.conf 的 http 中加入以下片断

```
# gzip config
    gzip on;
    gzip_min_length 1k;
    gzip_comp_level 9;
    gzip_types text/plain application/javascript application/x-javascript text/css application/xml text/javascript application/x-httpd-php image/jpeg image/gif image/png;
    gzip_vary on;
    gzip_disable "MSIE [1-6]\.";
```

## linux查看当前目录下，各文件夹大小

```
du -lh --max-depth=1
```



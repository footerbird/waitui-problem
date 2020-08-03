## NUXT pm2发布


PM2 是一个基于Node的，对前端服务的线程管理的服务器，而且自带负载均衡；
它能够作为服务端使用，映射静态文件为网站；他开启一个进程，指定一个默认的端口，同时能够在进程中开启多个线程，做自动的负载均衡；


参考地址
[https://www.liqinglin0314.com/article/241](https://www.liqinglin0314.com/article/241)


### 1.打包4个文件 命令 npm run build

a)nuxt.config.js

b)packge.json

c)static/

d).nuxt/

e)ui-domain/

### 2.把文件放在指定文件夹下

### 3.确保环境，安装npm，安装pm2 

```
yum install npm
npm install -g pm2
```

使用 npm -v; node -v; pm2 -v 能看到正常信息即可;

### 4.在文件夹中 npm install ，安装npm依赖

### 5.在文件夹中 【pm2 start npm --name  “项目别名” -- run start】 启动pm2的一个线程（可以启动多个）

### 6.现在已经可以直接用localhost:3000 访问了

### 7.配置Nginx反向代理，将3000端口代理到域名

## PM2 其他命令

pm2 stop all 停止所有服务

pm2 ls 查看所有服务

pm2 restart all 重启所有

pm2 start name 启动某个

pm2 delete all 删除所有

## 其他问题：

1.启动的时候“packge.json 中的name” 要把引号换成英文小写引号

2.启动不要切换root用户权限，可能会开两份，重新发布没法更新

3.nuxt项目的默认主机端口是localhost:3000，更改主机端口只需要在package.json中添加如下代码：

```
"config": {
  "nuxt": {
    "host": "0.0.0.0",
    "port": 3000
  }
},
```


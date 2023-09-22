## 一、下载相应版本的nodejs
```
https://nodejs.org/download/release/v12.20.0/
```
下载其中的linux版本的文件node-v12.20.0-linux-x64.tar.gz

## 二、将文件上传至服务器相应目录(在根目录创建nodejs目录)并解压，就得到了解压后的目录node-v12.20.0-linux-x64
```
tar -xzvf node-v12.20.0-linux-x64.tar.gz
```
此外，下面是压缩文件代码(对www文件夹进行压缩)
```
tar -czvf www.tar.gz ./www
```
### 三、修改/etc/profile配置环境变量
```
vim /etc/profile
1.按 i 建进入插入编辑状态
2.在文件最后加上一行：
  export PATH=/nodejs/node-v12.20.0-linux-x64/bin:$PATH
3. 按 Esc 退出编辑模式
4. 按 :wq！退出并保存文件
5. 用下面命令刷新环境变量
source /etc/profile
```
当然也可以用配置软链接的形式（相当于window的快捷方式），但是这样会有一个麻烦，就是npm每次全局安装一个工具，都得建一次软链接
```
ln -s /nodejs/node-v12.20.0-linux-x64/bin/node /usr/local/bin/node
ln -s /nodejs/node-v12.20.0-linux-x64/bin/npm /usr/local/bin/npm
ln -s /nodejs/node-v12.20.0-linux-x64/bin/yarn /usr/local/bin/yarn
...
```

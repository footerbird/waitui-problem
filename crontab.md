# crontab Linux创建定时器(以抓取快讯为例)

1. 创建sh文件并编辑需要执行的脚本

```
cd /var/www/html
touch flash.sh
vim flash.sh

#! /bin/bash
# 每隔2小时获取一次36kr快讯
curl https://admin.waitui.com/admin/Article_controller/batch_spider_flash_do
echo -e "\n快讯爬取成功..."
currTime=$(date +"%Y-%m-%d %T")
echo $currTime
```

2. 给脚本文件赋予权限

```
chmod -R 777 flash.sh
```

3. 查看系统中正在执行的定时器

```
crontab -l
```
可以看到当前有两个定时任务
```
*/1 * * * * /usr/local/qcloud/stargate/admin/start.sh > /dev/null 2>&1 &
0 0 * * * /usr/local/qcloud/YunJing/YDCrontab.sh > /dev/null 2>&1 &
```
这里的 * * * * *分别表示为分 小时 日 月 星期几

格式如下
```
f1 f2 f3 f4 f5 program
```
其中 f1 是表示分钟，f2 表示小时，f3 表示一个月份中的第几日，f4 表示月份，f5 表示一个星期中的第几天。program 表示要执行的程序。

当 f1 为 * 时表示每分钟都要执行 program，f2 为 * 时表示每小时都要执行程序，其馀类推

当 f1 为 a-b 时表示从第 a 分钟到第 b 分钟这段时间内要执行，f2 为 a-b 时表示从第 a 到第 b 小时都要执行，其馀类推

当 f1 为 */n 时表示每 n 分钟个时间间隔执行一次，f2 为 */n 表示每 n 小时个时间间隔执行一次，其馀类推

当 f1 为 a, b, c,... 时表示第 a, b, c,... 分钟要执行，f2 为 a, b, c,... 时表示第 a, b, c...个小时要执行，其馀类推


4. 添加定时器

```
crontab -e
```

打开了定时器编辑器，往编辑器中加入新的定时任务

```
*/1 * * * * /usr/local/qcloud/stargate/admin/start.sh > /dev/null 2>&1 &
0 0 * * * /usr/local/qcloud/YunJing/YDCrontab.sh > /dev/null 2>&1 &
0 */2 * * * /var/www/html/flash.sh >> /var/www/html/flash.log 2>&1 &
```

这里>> /var/www/html/flash.log表示将执行结果输出到flash.log文件中，>>表示如果文件已存在则向文件追加新添加的内容， 2>&1表示将错误结果也输出到log文件

可以看到里面多加了一个flash定时任务,然后保存重启就可以了

```
service crond restart
```

参考资料 [https://www.runoob.com/linux/linux-comm-crontab.html](https://www.runoob.com/linux/linux-comm-crontab.html)

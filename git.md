## 一、导出git不同版本之间的差异文件
```
git log --pretty=oneline
git diff dd67212 ee25971 --name-only | xargs zip update.zip
```
update.zip就是导出文件的压缩包

## 二、从远程拉取特定分支

```
git checkout -b develop origin/develop
```

## 三、将不同仓库的远程分支进行合并

关联远程仓库
```
git remote add bossure https://git.kaifazhe.me/laobanfx/shop/shop-b2b2c-web.git
```

删除远程仓库关联
```
git remote remove bossure
```

流程如下
```
git remote add bossure https://git.kaifazhe.me/laobanfx/shop/shop-b2b2c-web.git
git pull bossure
git checkout -b hotfix_7.2.0 bossure/hotfix_7.2.0
git checkout master
git merge hotfix_7.2.0
```

## 四、refusing to merge unrelated histories的解决方案

如果git merge合并的时候出现refusing to merge unrelated histories的错误，原因是两个仓库不同而导致的，需要在后面加上--allow-unrelated-histories进行允许合并，即可解决问题

```
git merge hotfix_7.2.0 --allow-unrelated-histories
```

## 五： 解决git pull时每次都要输入用户名密码的问题

```
https://footerbird:footerbirdxxxx@gitee.com/footerbird/ransheng-ad-landing.git
```
## 六、linux安装git
```
yum install git
```

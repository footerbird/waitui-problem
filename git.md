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

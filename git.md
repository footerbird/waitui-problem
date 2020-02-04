## 一、导出git不同版本之间的差异文件
```
git log --pretty=oneline
git diff dd67212 ee25971 --name-only | xargs zip update.zip
```
update.zip就是导出文件的压缩包

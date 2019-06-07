## --save和--save-dev的区别

npm install --save 局部安装，并会把模块自动写如入package.json中的dependencies（生产环境）里。

npm install --dev局部安装，并会把模块自动写入package.json中的devDependencies（开发环境，安装的是开发时需要的包。。。）里。

npm 5 开始 通过npm install不加--save 和npm install --save一样 都是局部安装并会把模块自动写入package.json中的dependencies里。

## package.json 与 package-lock.json 的区别

package.json 这个文件是 npm init 时创建的一个文件，会记录当前整个项目中的一些基础信息。而 package-lock.json 这个文件却是 node_modules 文件夹或者 package.json 文件发生变化时自动生成的。这个文件主要功能是确定当前安装的包的依赖，以便后续重新安装的时候生成相同的依赖，而忽略项目开发过程中有些依赖已经发生的更新。

自npm 5.0版本发布以来，npm i的规则发生了三次变化。

1、npm 5.0.x 版本，不管package.json怎么变，npm i 时都会根据lock文件下载[package-lock.json file not updated after package.json file is changed · Issue #16866 · npm/npm](https://github.com/npm/npm/issues/16866)这个 issue 控诉了这个问题，明明手动改了package.json，为啥不给我升级包！然后就导致了5.1.0的问题...

2、5.1.0版本后 npm install 会无视lock文件 去下载最新的npm[why is package-lock being ignored? · Issue #17979 · npm/npm](https://github.com/npm/npm/issues/17979)这个issue控诉这个问题，最后演变成5.4.2版本后的规则。

3、5.4.2版本后[why is package-lock being ignored? · Issue #17979 · npm/npm](https://github.com/npm/npm/issues/17979)

  大致意思是，如果改了package.json，且package.json和lock文件不同，那么执行`npm i`时npm会根据package中的版本号以及语义含义去下载最新的包，并更新至lock。

  如果两者是同一状态，那么执行`npm i `都会根据lock下载，不会理会package实际包的版本是否有新。



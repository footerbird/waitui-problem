# 利用electron结合vue开发web桌面应用

## 开发前的环境搭建和工具准备

1. nodejs、npm/cnpm/yarn、@vue/cli脚手架

2. 全局安装electron
```
cnpm install -g electron
electron -v
```

3. 全局安装electron-packager
```
cnpm install -g electron-packager
```

## 创建vue项目electron-rxgmy

```
vue create electron-rxgmy
cd electron-rxgmy
yarn
```
或
```
vue ui
```

在创建好的项目中添加vue.config.js
```
module.exports = {
  publicPath: './', // 改为相对路径
  assetsDir: 'static', // 静态资源路径
};
```

本地查看项目
```
yarn serve
```
如果没有问题的话，开始进行打包
```
yarn build
```

## 添加main.js主脚本文件和package.json文件

打包完成后，在项目文件夹中会出现一个dist目录，其中static是静态资源文件目录。在dist目录添加main.js文件和package.json文件

main.js
```
// Modules to control application life and create native browser window
const {app, BrowserWindow} = require('electron')
const path = require('path')

function createWindow () {
  // Create the browser window.
  const mainWindow = new BrowserWindow({
    width: 800,
    height: 600
  })

  // and load the index.html of the app.
  mainWindow.loadFile('index.html')

  // Open the DevTools.
  // mainWindow.webContents.openDevTools()
}

// This method will be called when Electron has finished
// initialization and is ready to create browser windows.
// Some APIs can only be used after this event occurs.
app.whenReady().then(() => {
  createWindow()
  
  app.on('activate', function () {
    // On macOS it's common to re-create a window in the app when the
    // dock icon is clicked and there are no other windows open.
    if (BrowserWindow.getAllWindows().length === 0) createWindow()
  })
})

// Quit when all windows are closed, except on macOS. There, it's common
// for applications and their menu bar to stay active until the user quits
// explicitly with Cmd + Q.
app.on('window-all-closed', function () {
  if (process.platform !== 'darwin') app.quit()
})

// In this file you can include the rest of your app's specific main process
// code. You can also put them in separate files and require them here.
```

package.json
```
{
  "name": "electron-rxgmy",
  "version": "1.0.0",
  "description": "A Electron Application For Rxgmy",
  "main": "main.js",
  "scripts": {
    "start": "electron .",
    "packager": "electron-packager ."
  },
  "author": "xf",
  "license": "CC0-1.0",
  "devDependencies": {
    "electron": "^11.1.0"
  }
}
```

安装依赖
```
cd dist
yarn
```

最后，本地运行electron项目
```
yarn start
```
这时一个electron应用程序窗口将会弹出

打包electron项目
```
yarn packager
```
在dist目录下将会生成一个electron-rxgmy-darwin-x64文件夹（这是mac系统生成应用程序的文件夹，windows系统文件夹名称不一样），生成的可执行文件就在该目录下

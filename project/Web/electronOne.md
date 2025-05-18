# Electron的基本使用

# 一、Electron的基本配置

## 1.1    创建项目

在终端输入`create-vue`，输入项目名称后，选择需要的功能

![image-20250512172348928](https://db.xinghai.ink/Typora/17470418315337226.png)

## 1.2    配置electron版本

electron是通过electron-builder构建成软件，所以electron和electron-builder的版本有要求，我这里两个都用最新版是会出错的，这里我就用我可以用的版本，其他版本可以继续尝试

选择package.json目录，添加下列参数就可以了

```json
  "devDependencies": {
    "electron": "^30.0.0",
    "electron-builder": "^24.13.3",
  },
```

接着运行npm i下载依赖

![image-20250512174513179](https://db.xinghai.ink/Typora/17470431157340748.png)

下载好后就可以了

## 1.3   配置electron命令和打包位置

在script中配置启动electron的命令

```json
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "preview": "vite preview",
    "start":"electron .",
    "pack":"electron-builder --dir"
  }
```

配置electron的打包位置，也就是electron软件的输出路径

```json
  "build":{
    "directories":{
      "output":"release"
    }
  }
```

整体的build配置如下

```json
"build": {
    "directories": {
      "output": "release"
    },
    "win": {
      "target": [
        {
          "target": "portable",
          "arch": [
            "x64"
          ]
        }
      ]
    },
    "nsis": {
      "oneClick": false,
      "perMachine": true,
      "allowToChangeInstallationDirectory": true
    }
  }
```

配置好后，在项目目录中创建main文件，输入以下内容

```js
const { app, BrowserWindow } = require('electron/main')

const createWindow = () => {
  const win = new BrowserWindow({
    width: 800,
    height: 600
  })

  win.loadFile('dist/index.html')
}

app.whenReady().then(() => {
  createWindow()

  app.on('activate', () => {
    if (BrowserWindow.getAllWindows().length === 0) {
      createWindow()
    }
  })
})
```


# electron-vue 尝试
当跑起来electron第一刻 我发现这个浏览器头是不是有点丑
是不是可以隐藏起来呢,答案当然是可以的

src/main/index.js
```
mainWindow = new BrowserWindow({
    height: 563,
    useContentSize: true,
    width: 1000,
    webPreferences: {webSecurity: false}, // 可实现跨域
    frame: false // 去掉浏览器头
  })
```
关闭后我发现不能关闭了，然后就解决一下

src/main/index.js
```
// 退出
ipcMain.on('window-all-closed', () => {
  app.quit()
})
// 小化
ipcMain.on('hide-window', () => {
  mainWindow.minimize()
})
// 最大化
ipcMain.on('show-window', () => {
  mainWindow.maximize()
})
// 还原
ipcMain.on('orignal-window', () => {
  mainWindow.unmaximize()
})
```
自己定义了一些控制按钮的样式
```
<div class="tools">
  <span class="tool-icon min"><i class="iconfont icon-zuixiaohua"></i></span>
  <span class="tool-icon max"><i class="iconfont icon-zuidahua"></i></span>
  <span class="tool-icon close"><i class="iconfont icon-guanbi"></i></span>
</div>
```

然后操作这些按钮，绑定对应事件

```
  import $ from 'jquery'
  var ipcRenderer = require('electron').ipcRenderer
  var isBig = true // 窗口放大还原标示
// 关闭窗口
  $(document).on('click', '.close', function () {
    console.log(1)
    ipcRenderer.send('window-all-closed')
  })
  // 最大化
  $(document).on('click', '.max', function () {
    if (isBig) {
      ipcRenderer.send('show-window')
    } else {
      ipcRenderer.send('orignal-window')
    }
    isBig = !isBig
  })
  // 最小化
  $(document).on('click', '.min', function () {
    ipcRenderer.send('hide-window')
  })

```

最后我希望点击头部可以拖拽(只需要给头部加上对应的样式)
```
-webkit-user-select: none;
-webkit-app-region: drag;
```
头部不想拖拽的部分
```
-webkit-app-region: no-drag;
```
关闭后托盘没有小图标 等一系列的问题
```
const url = path.join(__dirname, '../../static/img/on.ico')
  // 系统托盘图标
  let tray = new Tray(url)
  // 鼠标放到系统托盘图标上时的tips;
  tray.setToolTip('圣诞音乐')
  // 图标的上下文菜单
  const contextMenu = Menu.buildFromTemplate(trayMenuTemplate)
  // 设置此图标的上下文菜单
  tray.setContextMenu(contextMenu)
  // 双击图片显示窗口
  tray.on('double-click', () => {
    mainWindow.show()
    mainWindow.focus()
  })

```

[demo地址]()


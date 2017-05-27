# Setup Environment
> Setup Electon Environment with <http://www.blog.bdauria.com/?p=806> 해당 링크의 문서를 참조하였습니다.

## Angular2-Electron 개발환경 구축하기
![](/assets/img/angular-cli.png)
Angular2와 Electron 개발환경을 구축하기 위해서 `Angular-CLI`를 설치해줍니다.

Angular CLI 는 기본 구조, 컴포넌트 생성, 빌드, 유닛테스트, 개발서버, 배포를 관리 할 수 있도록 도와주는 커멘드라인 인터페이스 입니다.

```Shell
$ npm install -g @angular/cli
```

## Electron 설치하기
```Shell
$ npm install -g electon
```

## Angular2 프로젝트 생성
```Shell
$ ng new Project-Name
```

## Electron 폴더 생성
```Shell
$ cd Project-Name && mkdir electron
```

## Electron 파일 생성
> <https://electron.atom.io/docs/tutorial/quick-start/> 링크 참조

Electron을 구동하기위해 electron 폴더에 아래와 같은 파일들을 생성합니다.

```
Project-Name/electron
├── electron.js
└── package.json
```


```js
// Project-Name/electron/electron.js

const {app, BrowserWindow} = require('electron')

// Keep a global reference of the window object, if you don't, the window will
// be closed automatically when the JavaScript object is garbage collected.
let win

function createWindow() {
  // Create the browser window.
  win = new BrowserWindow({width: 800, height: 600})

  // and load the index.html of the app.
  win.loadURL(`file://${__dirname}/index.html`)

  // Open the DevTools.
  win.webContents.openDevTools()

  // Emitted when the window is closed.
  win.on('closed', () => {
    // Dereference the window object, usually you would store windows
    // in an array if your app supports multi windows, this is the time
    // when you should delete the corresponding element.
    win = null
  })
}

// This method will be called when Electron has finished
// initialization and is ready to create browser windows.
// Some APIs can only be used after this event occurs.
app.on('ready', createWindow)

// Quit when all windows are closed.
app.on('window-all-closed', () => {
  // On macOS it is common for applications and their menu bar
  // to stay active until the user quits explicitly with Cmd + Q
  if (process.platform !== 'darwin') {
    app.quit()
  }
})

app.on('activate', () => {
  // On macOS it's common to re-create a window in the app when the
  // dock icon is clicked and there are no other windows open.
  if (win === null) {
    createWindow()
  }
})

// In this file you can include the rest of your app's specific main process
// code. You can also put them in separate files and require them here.

```

```json
// src/electron/package.json
{
  "name"    : "angular-electron",
  "version" : "0.1.0",
  "main"    : "electron.js"
}
```




Angular2와 Electron의 작업 환경을 만들기 위하여 미리 만들어져 있는 Boilerplate Code를 git clone하여 가져옵니다.

Angular-Electron URL: [https://github.com/DenisVuyka/ng2-electron](https://github.com/DenisVuyka/ng2-electron)

> 주의! Angular Organization에서 제공하는 Angular-Electron의 Repository의 경우에는 2017.03.23일자 기준으로 현재 치명적인 오류가 있어, 코드를 사용할 수 없습니다.

```
$ git clone https://github.com/DenisVuyka/ng2-electron
$ cd ng2-electron
$ npm install
$ npm start
```
<http://projectl33t.xyz/archives/255>

# Electron에서 jQuery를 로드하는 방법
기타 다른 라이브러리와 다르게 jQuery의 경우에는 Electron 환경을 크롬과 다른 환경으로 인식, Common JS환경으로 인식하기 때문에 jQuery를 전역변수로 설정하지 않는다 따라서 jQuery를 Electron에서 사용하기 위해서는 별도의 설정이 필요합니다.

npm에서 jQuery를 설정했다면 이와 같이 설정하면 된다.
```javascript
window.$ = window.jQuery = require('jquery');
```

# Setup Environment
> Setup Electon Environment with <http://www.blog.bdauria.com/?p=806> 해당 링크의 문서를 참조하였습니다.

## Angular2-Electron 개발환경 구축하기
![](/assets/img/angular-cli.png)
Angular2와 Electron 개발환경을 구축하기 위해서 `Angular-CLI`를 설치해줍니다.

Angular CLI 는 기본 구조, 컴포넌트 생성, 빌드, 유닛테스트, 개발서버, 배포를 관리 할 수 있도록 도와주는 커멘드라인 인터페이스 입니다.

### Angular-CLI 설치하기
```Shell
$ npm install -g @angular/cli
```

### Electron 설치하기
```Shell
$ npm install -g electon
```

### Angular2 프로젝트 생성
```Shell
$ ng new Project-Name
```

### Electron 폴더 생성
```Shell
$ cd Project-Name && mkdir electron
```

### Electron 파일 생성
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

### base 링크 변경
`/src/index.html`의 `<base href="/">`를 `<base href="./">`으로 변경해줍니다.

```html
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>Practice05</title>
  <!-- 이 부분을 변경해줍니다 -->
  <base href="./">

  <meta name="viewport" content="width=device-width, initial-scale=1">
  <link rel="icon" type="image/x-icon" href="favicon.ico">
</head>
<body>
  <app-root>Loading...</app-root>
</body>
</html>
```

### npm 실행 명령어 설정
`/package.json`에서 npm으로 `electron`실행 명령어를 만들어 줍시다.

> `/electron/package.json`과 혼동하지 않도록 조심합니다.

```json
...
"scripts": {
    "ng": "ng",
    "start": "ng serve",
    "build": "ng build",
    "test": "ng test",
    "lint": "ng lint",
    "e2e": "ng e2e",
    "electron": "cp electron/* dist/ && electron dist/"
  },
...

```

### 실행하기
```Bash
$ ng build --watch
$ npm run electron
```

![](/assets/capture/helloworld.png)


### 빠른 설치
미리 만들어 놓은 Boilerplate 코드를 이용하여 쉽게 개발환경을 설정할 수 있습니다.

Boilerplate URL: <https://github.com/MSP-typescript/AngularCLI-Electron-Boilerplate>

```Bash
$ git clone https://github.com/MSP-typescript/AngularCLI-Electron-Boilerplate Project-Name
```

# Setup Libraries
Electron으로 개발하기에 앞서 디자인을 도와줄 `Semantic-UI`와 `jQuery`를 설치하는 법을 배워보도록 합시다.

### Electron에서 jQuery를 로드하는 방법
기타 다른 라이브러리와 다르게 jQuery의 경우에는 Electron 환경을 크롬과 다른 환경으로 인식, Common JS환경으로 인식하기 때문에 jQuery를 전역변수로 설정하지 않는다 따라서 jQuery를 Electron에서 사용하기 위해서는 별도의 설정이 필요합니다.

npm에서 jQuery를 설정했다면 이와 같이 설정하면 됩니다.

```Bash
$ npm install jquery
```

```javascript
window.$ = window.jQuery = require('jquery');
```

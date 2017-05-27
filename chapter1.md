# Setup Environment
## Angular2-Electron 개발환경 구축하기

Angular2와 Electron 개발환경을 구축하기 위해서 `Angular-CLI`를 설치해줍니다.

Angular CLI 는 기본 구조, 컴포넌트 생성, 빌드, 유닛테스트, 개발서버, 배포를 관리 할 수 있도록 도와주는 커멘드라인 인터페이스 입니다.

```Shell
$ npm install -g @angular/cli
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

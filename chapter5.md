# WebCAM
이번에는 `HTML5`에서 지원하는 `getUserMedia`를 이용해서 화면상에 WebCAM을 띄워보도록 하겠습니다.

웹캠으로 찍히는 화면이 App 내에서 표시될 `<video>`태그를 하나 만들어 줍니다.

#### app.component.html
```html
<div class="ui container">
  <h2 class="ui center aligned icon header">
    <img class="ui image" src="./assets/img/electron_icon.png">
    <div class="content">
      {{title}}
      <div class="sub header">{{subTitle}}</div>
    </div>
  </h2>
  <!-- 이 부분을 추가해 줍니다. -->
  <video id="camera" class="ui fluid" autoplay> </video>
</div>
```

그리고 이제 저 `<video>` 태그에 웹캠 화면을 띄워보도록 하겠습니다.

가장 먼저 `ngAfterViewInit()`이라는 `Lifecycle` 훅을 하나 만들어 줍니다.
`ngAfterViewInit()`를 쓰는 이유는 `View`가 초기화 된 이후에 `DOM Element`에 접근할 수 있기 때문입니다.

> Angular2의 Lifecycle의 내용은 ()<https://angular.io/docs/ts/latest/guide/lifecycle-hooks.html>를 참조하세요.

#### app.component.ts
```typescript
// ngAfterViewInit()을 쓰기 위해서 AfterViewInit을 import 해줍니다.
import { Component, AfterViewInit } from '@angular/core';
```

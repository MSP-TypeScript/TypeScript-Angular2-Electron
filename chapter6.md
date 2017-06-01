# Capture WebCAM stream
이번에는 WebCAM stream을 `Capture`하는 방법을 살펴보도록 하겠습니다.

일단 `app.component.html`에 캡쳐된 내용이 표시될 `<canvas>` 태그와 캡쳐버튼을 만들어 줍니다.

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
  <video id="camera" class="ui fluid" autoplay> </video>
  <!-- 이 부분을 추가해 줍니다. -->
  <div>
    <button id="btn_photo" class="ui button" (click)="takePhoto()">
      <i class="icon photo"></i>
      Take a Photo!
    </button>
  </div>
  <canvas id="myCanvas"></canvas>
</div>
```

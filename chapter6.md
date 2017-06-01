# Capture WebCAM stream
이번에는 WebCAM stream을 `Capture`하는 방법을 살펴보도록 하겠습니다.

일단 `app.component.html`에 캡쳐버튼과 캡쳐된 내용이 표시될 `<canvas>` 태그를 만들어 줍니다.

### Make Capture Button
먼저 캡쳐버튼을 만들어 보도록하겠습니다.

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
  <button id="btn_photo" class="ui fluid button" (click)="takePhoto()">
    <i class="icon photo"></i>
    Take a Photo!
  </button>
  <canvas id="myCanvas" class="ui fluid" width="640" height="480"></canvas>
</div>
```

#### app.component.css
```css
#camera{
  transform: scaleX(-1);
}

.fluid {
  margin-bottom: 20px;
  width: 100%;
}
```

이와 같이 잘 따라오셨다면 아래와 같은 화면이 나오게됩니다.

![](./assets/capture/makeCaptureBtn.png)

### Show the capture image in Canvas
다음은 캡처버튼이 클릭되었을 때 캡쳐된 내용을 `<canvas>` 태그에 표시하는 작업을 해보겠습니다.

먼저 `app.component.ts`를 열어서 `canvas`와 canvas의 내용이 들어갈 `ctx`를 멤버 변수로 선언해줍니다. 그 다음 데이터가 들어갈 수 있도록 아래와 같은 작업을 해줍니다.

#### app.component.ts
```typescript
...
export class AppComponent implements AfterViewInit {
  private title = 'Electron with Angular2';
  private subTitle = 'This app was made for Electron Angular Example';

  private video;
  private canvas;
  private ctx;

  ngAfterViewInit() {
    // canvas 초기화
    this.canvas = document.getElementById('myCanvas');
    // ctx 초기화
    this.ctx = this.canvas.getContext('2d');

    // ctx 좌우 반전
    this.ctx.translate(this.canvas.width, 0);
    this.ctx.scale(-1, 1);

    navigator.getUserMedia({ video: true, audio: false },
      (stream) => {
        this.video = document.getElementById('camera');
        this.video.srcObject = stream;
      },
      function (error) { console.log('error' + error); }
    );
  }

  // btn_photo에 바인딩할 takePhoto() 함수 정의하기
  takePhoto = () => {
    // 캡쳐된 화면 그리기
    this.ctx.drawImage(this.video, 0, 0, this.canvas.width, this.canvas.height);
  }
...
```

![](./assets/capture/capture.png)

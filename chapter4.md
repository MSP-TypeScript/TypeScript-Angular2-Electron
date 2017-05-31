# Build Structure
이제 본격적인 `App`의 구조를 잡아보도록 하겠습니다.

`app.component.html`의 파일을 열어서 다음과 같이 수정합니다.

```html
<!-- app.component.html -->
<div class="ui container">
  <h2 class="ui center aligned icon header">
    <img class="ui image" src="./assets/img/electron_icon.png">
    <div class="content">
      {{title}}
      <div class="sub header">{{subTitle}}</div>
    </div>
  </h2>
</div>
```

#### 첨부 1 electron_icon.png
![](./assets/img/electron_icon.png)

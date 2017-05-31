# Start Electron
이제 드디어 `Electron`으로 개발할 준비가 모두 완료되었습니다. 이제 본격적으로 개발을 시작해볼까요?

### Generating Button
일단 기본적인 `button`을 만들어보도록 하겠습니다.

`/src/app/app.component.html`파일을 열어줍니다. 그리고 `Semantic-UI`를 이용해서 간단한 버튼을 만들어봅시다.

```html
<!-- /src/app/app.component.html -->
<h1>
  {{title}}
</h1>
<button class="ui button">Button</button>
```

![](./assets/capture/makebutton.png)

이렇게 간단히 버튼이 생성이 된 것을 확인할 수 있습니다.

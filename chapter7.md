# Cognitive with HTTP

이번 문서에서는 `Angular2`에서 `HTTP` 통신을 이용하여 `Cognitive API`를 사용하는 방법을 소개하도록 하겠습니다.

> Cognitive API는 <https://azure.microsoft.com/en-us/try/cognitive-services/>에서 KEY를 발급받을 수 있습니다.

### Service 모듈 만들기
`Angular2`에서 `HTTP` 통신을 이용하기 위해서는 `Service`를 만들어야합니다.

`/src/app/`폴더에 `app.service.ts`를 하나 만들어 줍니다.

#### app.service.ts
```typescript
import { Injectable } from '@angular/core';
import { Headers, Http } from '@angular/http';

@Injectable()
export class AppService {

  constructor(private http: Http) {

  }

  faceRequest(url: string, img) {
    const headers = new Headers();
    headers.append('Content-Type', 'application/octet-stream');
    headers.append('Ocp-Apim-Subscription-Key', 'YOUR_API_KEY');
    return this.http.post(url, img, {headers: headers});
  }

  emotionRequest(url: string, img) {
    const headers = new Headers();
    headers.append('Content-Type', 'application/octet-stream');
    headers.append('Ocp-Apim-Subscription-Key', 'YOUR_API_KEY');
    return this.http.post(url, img, {headers: headers});
  }

}
```
> YOUR_API_KEY 부분에 자신이 발급받은 API KEY를 채워 넣어 줍니다.

### Service 모듈 등록하기
만든 `Service`모듈을 이제 등록시켜줍니다.

#### app.module.ts
```typescript
...
// Appservice 를 import 한 뒤
import { AppService } from './app.service';
...

@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    FormsModule,
    HttpModule
  ],
  // providers에 AppService를 등록해줍니다.
  providers: [AppService],
  bootstrap: [AppComponent]
})

export class AppModule { }
```

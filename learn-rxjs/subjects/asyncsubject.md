# AsyncSubject

## 완료 시 마지막 값 전달

### 예시

#### 예시 1: 간단한 AsyncSubject

\( [Stackblitz](https://stackblitz.com/edit/rxjs-asyncsubject?file=index.ts&devtoolsheight=100) \)

```javascript
// RxJS v6+
import { AsyncSubject } from 'rxjs';

const sub = new AsyncSubject();

sub.subscribe(console.log);

sub.next(123); //아무 로그도 찍히지 않음

sub.subscribe(console.log);

sub.next(456); //아무 로그도 찍히지 않음
sub.complete(); //양 쪽의 subscribers로부터 456, 456 로그가 찍힘
```

### 추가 자료

* [AsyncSubject](https://rxjs-dev.firebaseapp.com/api/index/class/AsyncSubject)  📰 - 공식 문서

> 📂 소스 코드: [https://github.com/ReactiveX/rxjs/blob/master/src/internal/AsyncSubject.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/AsyncSubject.ts)


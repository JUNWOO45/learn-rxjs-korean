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

sub.next(123); //nothing logged

sub.subscribe(console.log);

sub.next(456); //nothing logged
sub.complete(); //456, 456 logged by both subscribers
```

### 추가 자료

* [AsyncSubject](https://rxjs-dev.firebaseapp.com/api/index/class/AsyncSubject)

  :newspaper: - 공식 문서

> :file\_folder: 소스 코드: [https://github.com/ReactiveX/rxjs/blob/master/src/internal/AsyncSubject.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/AsyncSubject.ts)


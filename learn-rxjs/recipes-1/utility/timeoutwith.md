# timeoutWith

#### signature: `timeoutWith(due: number | Date, withObservable: ObservableInput, scheduler: SchedulerLike = async): OperatorFunction`

## 주어진 시간 범위 내에서 값이 내보내지지 않는다면, 두번째 옵저버블을 Subscribe합니다.

### 예시

**예시 1: 1초 후 Timeout**

\( [StackBlitz](https://stackblitz.com/edit/rxjs-timeoutwith?file=index.ts&devtoolsheight=100) \)

```javascript
// RxJS v6+
import { of } from 'rxjs';
import { timeoutWith, delay, concatMap } from 'rxjs/operators';

const fakeRequest = delayTime => of('!response!').pipe(delay(delayTime));
const requestTimeoutLogger = of('logging request timeout');
const timeoutThreshold = 1000;

of(timeoutThreshold + 1, timeoutThreshold - 1, timeoutThreshold + 3)
  .pipe(
    concatMap(e =>
      fakeRequest(e).pipe(timeoutWith(timeoutThreshold, requestTimeoutLogger))
    )
  )
  .subscribe(console.log);

/*
  결과:
    logging request timeout
    !response!
    logging request timeout
*/
```

### 추가 자료

* [timeoutWith](https://rxjs-dev.firebaseapp.com/api/operators/timeoutWith)

  :newspaper: - 공식 문서

> :file\_folder: Source Code: [https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/timeoutWith.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/timeoutWith.ts)


# timeout

#### signature: `timeout(due: number, scheduler: Scheduler): Observable`

## 지정된 기간 전에 값이 방출되지 않는 경우, 에러를 발생

### 예시

**예시 1: 2.5초 뒤에 Timeout**

\( [StackBlitz](https://stackblitz.com/edit/typescript-eegqyz?file=index.ts&devtoolsheight=100) \| [jsBin](http://jsbin.com/gonakiniho/edit?js,console) \| [jsFiddle](https://jsfiddle.net/btroncone/nr4e1ofy/1/) \)

```javascript
// RxJS v6+
import { of } from 'rxjs';
import { concatMap, timeout, catchError, delay } from 'rxjs/operators';

// 요청을 수행하는 함수
function makeRequest(timeToDelay) {
  return of('Request Complete!').pipe(delay(timeToDelay));
}

of(4000, 3000, 2000)
  .pipe(
    concatMap(duration =>
      makeRequest(duration).pipe(
        timeout(2500),
        catchError(error => of(`Request timed out after: ${duration}`))
      )
    )
  )
  /*
   *  "Request timed out after: 4000"
   *  "Request timed out after: 3000"
   *  "Request Complete!"
   */
  .subscribe(val => console.log(val));
```

### 추가 자료

* [timeout](https://rxjs.dev/api/operators/timeout)📰 - 공식 문서

> 📂 Source Code: [https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/timeout.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/timeout.ts)


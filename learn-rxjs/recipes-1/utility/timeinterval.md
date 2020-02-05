# timeInterval

#### signature: `timeInterval(scheduler: *): Observable<TimeInterval<any>> | WebSocketSubject<T> | Observable<T>`

## 내보내진 값들 사이의 경과된 시간을 변환합니다.

### 예시

**예시 1: 마우스 클릭 사이의 시간**

\( [StackBlitz](https://stackblitz.com/edit/rxjs-time-interval?file=index.ts&devtoolsheight=50) \)

```javascript
// RxJS v6+
import { fromEvent } from 'rxjs';
import { timeInterval, tap } from 'rxjs/operators';

fromEvent(document, 'mousedown')
  .pipe(
    timeInterval(),
    tap(console.log)
  )
  .subscribe(
    i =>
      (document.body.innerText = `milliseconds since last click: ${i.interval}`)
  );
```

### 관련된 사용법

* [Click Ninja Game](../../recipes/click-ninja-game.md)

### 추가 자료

* [timeInterval](https://rxjs.dev/api/operators/timeInterval)📰 - 공식 문서

> 📂 Source Code: [https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/timeInterval.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/timeInterval.ts)


# toArray

#### signature: `toArray(): OperatorFunction`

## 방출되는 값들을 모은 후, 소스 옵저버블 구독이 완료되면 배열형태로 내보냅니다.

### 예시

**예시 1: 시간 간격을 두고 방출되는 값을 모으고, 인터벌이 완료되면 배열형태로 내보냅니다**

\( [StackBlitz](https://stackblitz.com/edit/rxjs-toarray?file=index.ts&devtoolsheight=100) \)

```javascript
// RxJS v6+
import { interval } from 'rxjs';
import { toArray, take } from 'rxjs/operators';

interval(100)
  .pipe(
    take(10),
    toArray()
  )
  .subscribe(console.log);

// 결과: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

### 관련된 사용법

* [Breakout Game](../../recipes/breakout-game.md)
* [Lockscreen](../../recipes/lockscreen.md)

### 추가 자료

* [toArray](https://rxjs.dev/api/operators/toArray) 📰 - 공식 문서

> 📂 Source Code: [https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/toArray.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/toArray.ts)


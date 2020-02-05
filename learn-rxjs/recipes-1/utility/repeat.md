# repeat

#### signature: `repeat(count: number): Observable`

## 완료 시 옵저버블을 반복합니다.

:bulb: [`retry`](../error_handling/retry.md)와 같지만, 에러가 없는 경우에만 반복합니다!

### 예시

**예시 1: 3번 반복합니다**

\( [StackBlitz](https://stackblitz.com/edit/rxjs-repeat-learnrxjs?file=index.ts&devtoolsheight=100) \)

```javascript
// RxJS v6+
import { repeat, delay } from 'rxjs/operators';
import { of } from 'rxjs';

const delayedThing = of('delayed value').pipe(delay(2000));

delayedThing
  .pipe(repeat(3))
  // delayed value.. delayed value.. delayed value..
  .subscribe(console.log);
```

### 관련된 사용법

* [Click Ninja Game](../../recipes/click-ninja-game.md)
* [Lockscreen](../../recipes/lockscreen.md)
* [Space Invaders Game](../../recipes/space-invaders-game.md)
* [Swipe To Refresh](../../recipes/swipe-to-refresh.md)

### 추가 자료

* [repeat](https://rxjs.dev/api/operators/repeat)

  :newspaper: - 공식 문서

> :file\_folder: Source Code: [https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/repeat.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/repeat.ts)


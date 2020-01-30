# takeWhile

#### signature: `takeWhile(predicate: function(value, index): boolean, inclusive?: boolean): Observable`

## 넘겨받은 표현식이 참인 동안, 값을 발생시킵니다.

💡 옵션 파라미터인 `inclusive` 가 `true` 로 지정되면, 참을 만족하지못하는 첫번째 아이템 또한 발생시킵니다.

### 예시

**예시 1: 조건에 해당하는 값만 받습니다**

\( [StackBlitz](https://stackblitz.com/edit/typescript-af3hdf?file=index.ts&devtoolsheight=100) \| [jsBin](http://jsbin.com/zanefaqexu/1/edit?js,console) \| [jsFiddle](https://jsfiddle.net/btroncone/yakd4jgc/) \)

```javascript
// RxJS v6+
import { of } from 'rxjs';
import { takeWhile } from 'rxjs/operators';

// 1,2,3,4,5를 발생시킵니다
const source$ = of(1, 2, 3, 4, 5);

//4 이하인 값만 발생시키고, 종료합니다
source$
  .pipe(takeWhile(val => val <= 4))
   // log: 1,2,3,4
  .subscribe(val => console.log(val));
```

**예시2: \(v6.4+\) inclusive를 활용한 takeWhile**

\( [StackBlitz](https://stackblitz.com/edit/typescript-3bwfup?file=index.ts&devtoolsheight=100) \)

```javascript
// RxJS v6.4+
import { of } from 'rxjs';
import { takeWhile, filter } from 'rxjs/operators';

const source$ = of(1, 2, 3, 9);

source$
  // inclusive 를 설정하면, false를 리턴하게 하는 값도 발생되어집니다
  .pipe(takeWhile(val => val <= 3, true))
  // log: 1, 2, 3, 9
  .subscribe(console.log);
```

**예시 3: takeWhile 과 filter의 차이점**

\( [StackBlitz](https://stackblitz.com/edit/typescript-roozza?file=index.ts&devtoolsheight=100) \| [jsBin](http://jsbin.com/yatoqurewi/1/edit?js,console) \| [jsFiddle](https://jsfiddle.net/r497jgw3/4/) \)

```javascript
// RxJS v6+
import { of } from 'rxjs';
import { takeWhile, filter } from 'rxjs/operators';

// 3, 3, 3, 9, 1, 4, 5, 8, 96, 3, 66, 3, 3, 3를 발생시킵니다
const source$ = of(3, 3, 3, 9, 1, 4, 5, 8, 96, 3, 66, 3, 3, 3);

// 소스의 값이 3일 때만 값을 발생시키고, 종료합니다
source$
  .pipe(takeWhile(it => it === 3))
  // log: 3, 3, 3
  .subscribe(val => console.log('takeWhile', val));

source$
  .pipe(filter(it => it === 3))
  // log: 3, 3, 3, 3, 3, 3, 3
  .subscribe(val => console.log('filter', val));
```

### 관련 사용법

* [Alphabet Invasion Game](../../recipes/alphabet-invasion-game.md)
* [Battleship Game](../../recipes/battleship-game.md)
* [Breakout Game](../../recipes/breakout-game.md)
* [Car Racing Game](../../recipes/car-racing-game.md)
* [Catch The Dot Game](../../recipes/catch-the-dot-game.md)
* [Click Ninja Game](../../recipes/click-ninja-game.md)
* [Flappy Bird Game](../../recipes/flappy-bird-game.md)
* [Mine Sweeper Game](../../recipes/mine-sweeper-game.md)
* [Platform Jumper Game](../../recipes/platform-jumper-game.md)
* [Smart Counter](../../recipes/smartcounter.md)
* [Swipe To Refresh](../../recipes/swipe-to-refresh.md)
* [Tetris Game](../../recipes/tetris-game.md)
* [Uncover Image Game](../../recipes/uncover-image-game.md)

### 추가 자료

* [takeWhile](https://rxjs-dev.firebaseapp.com/api/operators/takeWhile) 📰 - 공식 문서
* [Completing a stream with takeWhile](https://egghead.io/lessons/rxjs-completing-a-stream-with-takewhile?course=step-by-step-async-javascript-with-rxjs) 📹💵 - John Linquist

> 📂 Source Code: [https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/takeWhile.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/takeWhile.ts)


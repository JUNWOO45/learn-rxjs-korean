# tap / do

#### signature: `tap(nextOrObserver: function, error: function, complete: function): Observable`

## 부작용없이 로깅과 같은 액션을 수행합니다.

:bulb: pipeable 연산자를 사용중이라면, `do` 대신  `tap` 을 사용하세요!

### 예시

**예시 1: tap을 사용하여 로그찍기**

\( [StackBlitz](https://stackblitz.com/edit/typescript-cd2gjp?file=index.ts&devtoolsheight=100) \| [jsBin](http://jsbin.com/jimazuriva/1/edit?js,console) \| [jsFiddle](https://jsfiddle.net/btroncone/qtyakorq/) \)

```javascript
// RxJS v6+
import { of } from 'rxjs';
import { tap, map } from 'rxjs/operators';

const source = of(1, 2, 3, 4, 5);
// 'tap'을 사용하여 소스로부터 로그 값을 찍습니다.
const example = source.pipe(
  tap(val => console.log(`BEFORE MAP: ${val}`)),
  map(val => val + 10),
  tap(val => console.log(`AFTER MAP: ${val}`))
);

//'tap'은 값을 바꾸지 않습니다.
//결과: 11...12...13...14...15
const subscribe = example.subscribe(val => console.log(val));
```

**예시 2: 객체에서 tap 사용하기**

\( [StackBlitz](https://stackblitz.com/edit/typescript-3xykpb?file=index.ts&devtoolsheight=100)\)

```javascript
// RxJS v6+
import { of } from 'rxjs';
import { tap, map } from 'rxjs/operators';

const source = of(1, 2, 3, 4, 5);

// tap은 next, error, complete을 사용할 수 있습니다
const example = source
  .pipe(
    map(val => val + 10),
    tap({
      next: val => {
        // on next 11 이 찍힙니다.
        console.log('on next', val);
      },
      error: error => {
        console.log('on error', error.message);
      },
      complete: () => console.log('on complete')
    })
  )
  // 결과: 11, 12, 13, 14, 15
  .subscribe(val => console.log(val));
```

### 관련된 사용법

* [Battleship Game](../../recipes/battleship-game.md)
* [Breakout Game](../../recipes/breakout-game.md)
* [Car Racing Game](../../recipes/car-racing-game.md)
* [Catch The Dot Game](../../recipes/catch-the-dot-game.md)
* [Click Ninja Game](../../recipes/click-ninja-game.md)
* [Flappy Bird Game](../../recipes/flappy-bird-game.md)
* [Horizontal Scroll Indicator](../../recipes/horizontal-scroll-indicator.md)
* [Lockscreen](../../recipes/lockscreen.md)
* [Memory Game](../../recipes/memory-game.md)
* [Mine Sweeper Game](../../recipes/mine-sweeper-game.md)
* [Platform Jumper Game](../../recipes/platform-jumper-game.md)
* \[Save Indicator\]\('../../recipes/save-indicator.md\)
* [Space Invaders Game](../../recipes/space-invaders-game.md)
* [Stop Watch](../../recipes/stop-watch.md)
* [Swipe To Refresh](../../recipes/swipe-to-refresh.md)
* [Tank Battle Game](../../recipes/tank-battle-game.md)
* [Tetris Game](../../recipes/tetris-game.md)
* [Type Ahead](../../recipes/type-ahead.md)
* [Uncover Image Game](../../recipes/uncover-image-game.md)

### 추가 자료

* [tap](https://rxjs.dev/api/operators/tap) :newspaper: - 공식 문서
* [Logging a stream with do](https://egghead.io/lessons/rxjs-logging-a-stream-with-do?course=step-by-step-async-javascript-with-rxjs)

  :video\_camera: :dollar: - John Linquist

* [Utility operator: do](https://egghead.io/lessons/rxjs-utility-operator-do?course=rxjs-beyond-the-basics-operators-in-depth)

  :video\_camera: :dollar: - André Staltz

* [Build your own tap operator](https://blog.strongbrew.io/build-the-operators-from-rxjs-from-scratch/?lectureId=tap#app)

  :video\_camera: - Kwinten Pisman

> :file\_folder: Source Code: [https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/do.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/do.ts)


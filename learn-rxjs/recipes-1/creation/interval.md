# interval

#### signature: `interval(period: number, scheduler: Scheduler): Observable`

## 주어진 시간에따라 연속된 수를 내보냅니다.

### 예시

**예시 1: 1초 간격으로 값을 내보냅니다.**

\( [StackBlitz](https://stackblitz.com/edit/typescript-ohddud?file=index.ts&devtoolsheight=100) \| [jsBin](http://jsbin.com/vigohomabo/1/edit?js,console) \| [jsFiddle](https://jsfiddle.net/btroncone/x3mrwzr0/) \)

```javascript
// RxJS v6+
import { interval } from 'rxjs';

//매 1초마다 연속해서 값을 내보냅니다.
const source = interval(1000);
//결과: 0,1,2,3,4,5....
const subscribe = source.subscribe(val => console.log(val));
```

### 관련된 사용법

* [Alphabet Invasion Game](../../recipes/alphabet-invasion-game.md)
* [Battleship Game](../../recipes/battleship-game.md)
* [Breakout Game](../../recipes/breakout-game.md)
* [Car Racing Game](../../recipes/car-racing-game.md)
* [Catch The Dot Game](../../recipes/catch-the-dot-game.md)
* [Flappy Bird Game](../../recipes/flappy-bird-game.md)
* [Matrix Digital Rain](../../recipes/matrix-digital-rain.md)
* [Memory Game](../../recipes/memory-game.md)
* [Platform Jumper Game](../../recipes/platform-jumper-game.md)
* [Space Invaders Game](../../recipes/space-invaders-game.md)
* [Stop Watch](../../recipes/stop-watch.md)
* [Tank Battle Game](../../recipes/tank-battle-game.md)
* [Tetris Game](../../recipes/tetris-game.md)
* [Uncover Image Game](../../recipes/uncover-image-game.md)

### 추가 자료

* [interval](https://rxjs.dev/api/index/function/interval)

  :newspaper: - 공식 문서

* [Creation operators: interval and timer](https://egghead.io/lessons/rxjs-creation-operators-interval-and-timer?course=rxjs-beyond-the-basics-creating-observables-from-scratch)

  :video\_camera: :dollar: - André Staltz

* [Build your own interval operator](https://blog.strongbrew.io/build-the-operators-from-rxjs-from-scratch/?lectureId=interval#app)

  :video\_camera: - Kwinten Pisman

> :file\_folder: Source Code: [https://github.com/ReactiveX/rxjs/blob/master/src/internal/observable/interval.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/observable/interval.ts)


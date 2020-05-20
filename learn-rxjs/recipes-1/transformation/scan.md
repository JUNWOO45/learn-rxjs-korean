# scan

#### signature: `scan(accumulator: function, seed: any): Observable`

## Reduce해나갑니다.

:bulb: scan을 활용하여 [Redux](http://redux.js.org)스러운 상태관리를 할 수 있습니다! 

### 예시

**예시 1: 더해나갑니다.**

\( [StackBlitz](https://stackblitz.com/edit/typescript-ltcl9d?file=index.ts&devtoolsheight=100) \)

```javascript
// RxJS v6+
import { of } from 'rxjs';
import { scan } from 'rxjs/operators';

const source = of(1, 2, 3);
// 간단한 scan 예시로, 0부터 시작해서 더해나갑니다.
const example = source.pipe(scan((acc, curr) => acc + curr, 0));
// 누적된 값을 기록합니다.
// output: 1,3,6
const subscribe = example.subscribe(val => console.log(val));
```

**예시 2: 객체에서 사용하기**

\( [StackBlitz](https://stackblitz.com/edit/typescript-vu63kz?file=index.ts&devtoolsheight=100) \| [jsBin](http://jsbin.com/fusunoguqu/1/edit?js,console) \| [jsFiddle](https://jsfiddle.net/btroncone/36rbu38b/) \)

```javascript
// RxJS v6+
import { Subject } from 'rxjs';
import { scan } from 'rxjs/operators';

const subject = new Subject();
// 객체를 만들어나가는 scan 예시
const example = subject.pipe(
  scan((acc, curr) => Object.assign({}, acc, curr), {})
);
//누적된 값을 기록합니다.
const subscribe = example.subscribe(val =>
  console.log('Accumulated object:', val)
);
// subject로 다음 값을 넘겨주고, 객체의 프로퍼티로 추가합니다
// {name: 'Joe'}
subject.next({ name: 'Joe' });
// {name: 'Joe', age: 30}
subject.next({ age: 30 });
// {name: 'Joe', age: 30, favoriteLanguage: 'JavaScript'}
subject.next({ favoriteLanguage: 'JavaScript' });
```

**예시 3: 누적된 배열에서 무작위 값을 내보냅니다.**

\( [StackBlitz](https://stackblitz.com/edit/typescript-lb8aw9?file=index.ts&devtoolsheight=100) \)

```javascript
// RxJS v6+
import { interval } from 'rxjs';
import { scan, map, distinctUntilChanged } from 'rxjs/operators';

// 배열에 값을 누적시키고, 무작위 값을 꺼냅니다.
const scanObs = interval(1000)
  .pipe(
    scan((a, c) => [...a, c], []),
    map(r => r[Math.floor(Math.random() * r.length)]),
    distinctUntilChanged()
  )
  .subscribe(console.log);
```

**예시 4: http 응답을 누적시킵니다**

\( [StackBlitz](https://stackblitz.com/edit/rxjs-scan-accumulate-request-responses?file=index.ts&devtoolsheight=100) \)

```javascript
// RxJS v6+
import { interval, of } from 'rxjs';
import { scan, delay, repeat, mergeMap } from 'rxjs/operators';

const fakeRequest = of('response').pipe(delay(2000));

// 결과:
// ['response'],
// ['response','response'],
// ['response','response','response'],
// etc...

interval(1000)
  .pipe(
    mergeMap(_ => fakeRequest),
    scan<string>((all, current) => [...all, current], [])
  )
  .subscribe(console.log);
```

### 관련된 사용법

* [Alphabet Invasion Game](../../recipes/alphabet-invasion-game.md)
* [Battleship Game](../../recipes/battleship-game.md)
* [Breakout Game](../../recipes/breakout-game.md)
* [Car Racing Game](../../recipes/car-racing-game.md)
* [Catch The Dot Game](../../recipes/catch-the-dot-game.md)
* [Click Ninja Game](../../recipes/click-ninja-game.md)
* [Flappy Bird Game](../../recipes/flappy-bird-game.md)
* [Matrix Digital Rain](../../recipes/matrix-digital-rain.md)
* [Memory Game](../../recipes/memory-game.md)
* [Platform Jumper Game](../../recipes/platform-jumper-game.md)
* [Progress Bar](../../recipes/progressbar.md)
* [Smart Counter](../../recipes/smartcounter.md)
* [Space Invaders Game](../../recipes/space-invaders-game.md)
* [Stop Watch](../../recipes/stop-watch.md)
* [Tank Battle Game](../../recipes/tank-battle-game.md)
* [Tetris Game](../../recipes/tetris-game.md)
* [Uncover Image Game](../../recipes/uncover-image-game.md)

### 추가 자료

* [scan](https://rxjs.dev/api/operators/scan)

  :newspaper: - 공식 문서

* [Aggregating streams with reduce and scan using RxJS](https://egghead.io/lessons/rxjs-aggregating-streams-with-reduce-and-scan-using-rxjs)

  :video\_camera: - Ben Lesh

* [Updating data with scan](https://egghead.io/lessons/rxjs-updating-data-with-scan?course=step-by-step-async-javascript-with-rxjs)

  :video\_camera: :dollar: - John Linquist

* [Transformation operator: scan](https://egghead.io/lessons/rxjs-transformation-operator-scan?course=rxjs-beyond-the-basics-operators-in-depth)

  :video\_camera: :dollar: - André Staltz

* [Build your own scan operator](https://blog.strongbrew.io/build-the-operators-from-rxjs-from-scratch/?lectureId=scan#app)

  :video\_camera: - Kwinten Pisman

> :file\_folder: Source Code: [https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/scan.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/scan.ts)


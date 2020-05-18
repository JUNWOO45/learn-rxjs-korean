# startWith

#### signature: `startWith(an: Values): Observable`

## 주어진 값을 처음으로 방출합니다.

:bulb: [BehaviorSubject](https://github.com/Reactive-Extensions/RxJS/blob/master/doc/api/subjects/behaviorsubject.md) 또한 초기값부터 시작할 수 있습니다!

### 예시

\( [예시 테스트](https://github.com/btroncone/learn-rxjs/blob/master/operators/specs/combination/startwith-spec.ts) \)

**예시 1: 연속된 숫자와 startWith 사용하기**

\( [StackBlitz](https://stackblitz.com/edit/typescript-2qrwjt?file=index.ts&devtoolsheight=100) \| [jsBin](http://jsbin.com/lezuravizu/1/edit?js,console) \| [jsFiddle](https://jsfiddle.net/btroncone/e8dn3ggp/) \)

```javascript
// RxJS v6+
import { startWith } from 'rxjs/operators';
import { of } from 'rxjs';

//방출 (1,2,3)
const source = of(1, 2, 3);
// 0부터 시작
const example = source.pipe(startWith(0));
//결과: 0,1,2,3
const subscribe = example.subscribe(val => console.log(val));
```

**예시 2: scan한 값과 startWith사용하기**

\( [StackBlitz](https://stackblitz.com/edit/typescript-8gkbsc?file=index.ts&devtoolsheight=100) \| \| [jsBin](http://jsbin.com/gemevuzoha/1/edit?js,console) \| [jsFiddle](https://jsfiddle.net/btroncone/54r3g83e/) \)

```javascript
// RxJS v6+
import { startWith, scan } from 'rxjs/operators';
import { of } from 'rxjs';

//방출 ('World!', 'Goodbye', 'World!')
const source = of('World!', 'Goodbye', 'World!');
// 'Hello'부터 시작하고, 이전값과 현재값 concat하기
const example = source.pipe(
  startWith('Hello'),
  scan((acc, curr) => `${acc} ${curr}`)
);
/*
  결과:
  "Hello"
  "Hello World!"
  "Hello World! Goodbye"
  "Hello World! Goodbye World!"
*/
const subscribe = example.subscribe(val => console.log(val));
```

**예시 3: 복수의 값들을 startWith로 사용하기**

\( [StackBlitz](https://stackblitz.com/edit/typescript-ek45ff?file=index.ts&devtoolsheight=100) \| [jsBin](http://jsbin.com/cumupemuxa/1/edit?js,console) \| [jsFiddle](https://jsfiddle.net/btroncone/ckcyj3ms/) \)

```javascript
// RxJS v6+
import { startWith } from 'rxjs/operators';
import { interval } from 'rxjs';

//매 1초마다 값 내보내기
const source = interval(1000);
// -3, -2, -1부터 시작하기
const example = source.pipe(startWith(-3, -2, -1));
//결과: -3, -2, -1, 0, 1, 2....
const subscribe = example.subscribe(val => console.log(val));
```

### 관련한 사용법

* [Alphabet Invasion Game](../../recipes/alphabet-invasion-game.md)
* [Breakout Game](../../recipes/breakout-game.md)
* [Car Racing Game](../../recipes/car-racing-game.md)
* [Platform Jumper Game](../../recipes/platform-jumper-game.md)
* [Smart Counter](../../recipes/smartcounter.md)
* [Space Invaders Game](../../recipes/space-invaders-game.md)
* [Stop Watch](../../recipes/stop-watch.md)
* [Tank Battle Game](../../recipes/tank-battle-game.md)
* [Tetris Game](../../recipes/tetris-game.md)
* [Uncover Image Game](../../recipes/uncover-image-game.md)

### 추가 자료

* [startWith](https://rxjs.dev/api/operators/startWith)

  :newspaper: - 공식 문서

* [Displaying initial data with startWith](https://egghead.io/lessons/rxjs-displaying-initial-data-with-startwith?course=step-by-step-async-javascript-with-rxjs)

  :video\_camera: :dollar: - John Linquist

* [Clear data while loading with startWith](https://egghead.io/lessons/rxjs-reactive-programming-clear-data-while-loading-with-rxjs-startwith?course=introduction-to-reactive-programming)

  :video\_camera: :dollar: - André Staltz

* [Combination operator: concat, startWith](https://egghead.io/lessons/rxjs-combination-operators-concat-startwith?course=rxjs-beyond-the-basics-operators-in-depth)

  :video\_camera: :dollar: - André Staltz

> :file\_folder: Source Code: [https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/startWith.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/startWith.ts)


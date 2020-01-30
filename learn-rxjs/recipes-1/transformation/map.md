# map

#### signature: `map(project: Function, thisArg: any): Observable`

## 각각의 값에 넘겨받은 콜백을 적용합니다.

### 예시

**예시 1: 각각의 숫자에 10을 더합니다**

\( [StackBlitz](https://stackblitz.com/edit/typescript-a7bnxb?file=index.ts&devtoolsheight=100) \| [jsBin](http://jsbin.com/padasukano/1/edit?js,console) \| [jsFiddle](https://jsfiddle.net/btroncone/yd38awLa/) \)

```javascript
// RxJS v6+
import { from } from 'rxjs';
import { map } from 'rxjs/operators';

//(1,2,3,4,5) 발생시킵니다
const source = from([1, 2, 3, 4, 5]);
//각각의 값에 10을 더합니다
const example = source.pipe(map(val => val + 10));
//결과: 11,12,13,14,15
const subscribe = example.subscribe(val => console.log(val));
```

**예시 2: 단일 프로퍼티에 map사용하기**

\( [StackBlitz](https://stackblitz.com/edit/typescript-qgpnju?file=index.ts&devtoolsheight=100) \| [jsBin](http://jsbin.com/detozumale/1/edit?js,console) \| [jsFiddle](https://jsfiddle.net/btroncone/tdLd5tgc/) \)

```javascript
// RxJS v6+
import { from } from 'rxjs';
import { map } from 'rxjs/operators';

// ({name: 'Joe', age: 30}, {name: 'Frank', age: 20},{name: 'Ryan', age: 50}) 를 발생시킵니다
const source = from([
  { name: 'Joe', age: 30 },
  { name: 'Frank', age: 20 },
  { name: 'Ryan', age: 50 }
]);
//name값만 가지고옵니다. 이번 예시에서는 pluck을 사용해도 같은 결과를 만들어낼 수 있습니다.
const example = source.pipe(map(({ name }) => name));
//결과: "Joe","Frank","Ryan"
const subscribe = example.subscribe(val => console.log(val));
```

### 관련된 사용법

* [Alphabet Invasion Game](../../recipes/alphabet-invasion-game.md)
* [Battleship Game](../../recipes/battleship-game.md)
* [Catch The Dot Game](../../recipes/catch-the-dot-game.md)
* [Game Loop](../../recipes/gameloop.md)
* [HTTP Polling](../../recipes/http-polling.md)
* [Lockscreen](../../recipes/lockscreen.md)
* [Memory Game](../../recipes/memory-game.md)
* [Mine Sweeper Game](../../recipes/mine-sweeper-game.md)
* \[Save Indicator\]\('../../recipes/save-indicator.md\)
* [Smart Counter](../../recipes/smartcounter.md)
* [Space Invaders Game](../../recipes/space-invaders-game.md)
* [Stop Watch](../../recipes/stop-watch.md)
* [Swipe To Refresh](../../recipes/swipe-to-refresh.md)
* [Tetris Game](../../recipes/tetris-game.md)
* [Type Ahead](../../recipes/type-ahead.md)

### 추가 자료

* [map](https://rxjs.dev/api/operators/map) :newspaper: - 공식 문서
* [map vs flatMap](https://egghead.io/lessons/rxjs-rxjs-map-vs-flatmap)

  :video\_camera: - Ben Lesh

* [Transformation operator: map and mapTo](https://egghead.io/lessons/rxjs-transformation-operator-map-and-mapto?course=rxjs-beyond-the-basics-operators-in-depth) :video\_camera: :dollar: - André Staltz
* [Build your own map operator](https://blog.strongbrew.io/build-the-operators-from-rxjs-from-scratch/?lectureId=map#app) :video\_camera: - Kwinten Pisman

> :file\_folder: Source Code: [https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/map.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/map.ts)


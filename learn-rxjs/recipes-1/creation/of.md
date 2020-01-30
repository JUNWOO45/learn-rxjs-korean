# of

#### signature: `of(...values, scheduler: Scheduler): Observable`

## 주어진 인자를 옵저버블로 바꿉니다.

### 예시

**예시 1: 순서대로 숫자를 내보냅니다.**

\( [StackBlitz](https://stackblitz.com/edit/typescript-kbpvmm?file=index.ts&devtoolsheight=100) \| [jsBin](http://jsbin.com/kodixitoji/1/edit?js,console) \| [jsFiddle](https://jsfiddle.net/btroncone/f7b35ayz/) \)

```javascript
// RxJS v6+
import { of } from 'rxjs';
//제공된 수를 순서대로 내보냅니다.
const source = of(1, 2, 3, 4, 5);
//결과: 1,2,3,4,5
const subscribe = source.subscribe(val => console.log(val));
```

**예시 2: 객체, 배열, 함수를 내보냅니다.**

\( [StackBlitz](https://stackblitz.com/edit/typescript-m1jbw9?file=index.ts&devtoolsheight=100) \| [jsBin](http://jsbin.com/xevobujama/1/edit?js,console) \| [jsFiddle](https://jsfiddle.net/btroncone/d9rng4dj/) \)

```javascript
// RxJS v6+
import { of } from 'rxjs';
//어떠한 타입의 값이든 내보냅니다.
const source = of({ name: 'Brian' }, [1, 2, 3], function hello() {
  return 'Hello';
});
//결과: {name: 'Brian'}, [1,2,3], function hello() { return 'Hello' }
const subscribe = source.subscribe(val => console.log(val));
```

### 관련된 사용법

* [Battleship Game](../../recipes/battleship-game.md)
* [Breakout Game](../../recipes/breakout-game.md)
* [Car Racing Game](../../recipes/car-racing-game.md)
* [Mine Sweeper Game](../../recipes/mine-sweeper-game.md)
* [Platform Jumper Game](../../recipes/platform-jumper-game.md)
* \[Save Indicator\]\('../../recipes/save-indicator.md\)
* [Swipe To Refresh](../../recipes/swipe-to-refresh.md)
* [Tetris Game](../../recipes/tetris-game.md)
* [Type Ahead](../../recipes/type-ahead.md)

### 추가 자료

* [of](https://rxjs.dev/api/index/function/of)

  :newspaper: - 공식 문서

* [Creation operators: of](https://egghead.io/lessons/rxjs-creation-operator-of?course=rxjs-beyond-the-basics-creating-observables-from-scratch)

  :video\_camera: :dollar: - André Staltz

* [Build your own of operator](https://blog.strongbrew.io/build-the-operators-from-rxjs-from-scratch/?lectureId=of#app)

  :video\_camera: - Kwinten Pisman

> :file\_folder: Source Code: [https://github.com/ReactiveX/rxjs/blob/master/src/internal/observable/of.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/observable/of.ts)


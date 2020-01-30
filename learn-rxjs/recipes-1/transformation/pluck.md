# pluck

#### signature: `pluck(properties: ...args): Observable`

## 값을 발생시킬 프로퍼티를 선택합니다

### 예시

**예시1: 객체 프로퍼티 뽑아내기**

\( [StackBlitz](https://stackblitz.com/edit/typescript-jkda4e?file=index.ts&devtoolsheight=100) \| [jsBin](http://jsbin.com/zokaxiwahe/1/edit?js,console) \| [jsFiddle](https://jsfiddle.net/btroncone/58v9xq0f/) \)

```javascript
// RxJS v6+
import { from } from 'rxjs';
import { pluck } from 'rxjs/operators';

const source = from([{ name: 'Joe', age: 30 }, { name: 'Sarah', age: 35 }]);
//names만 가져옵니다
const example = source.pipe(pluck('name'));
//결과: "Joe", "Sarah"
const subscribe = example.subscribe(val => console.log(val));
```

**예시 2: nested 프로퍼티 뽑아내기**

\( [StackBlitz](https://stackblitz.com/edit/typescript-rinjzk?file=index.ts&devtoolsheight=100) \| [jsBin](http://jsbin.com/joqesidugu/1/edit?js,console) \| [jsFiddle](https://jsfiddle.net/btroncone/n592m597/) \)

```javascript
// RxJS v6+
import { from } from 'rxjs';
import { pluck } from 'rxjs/operators';

const source = from([
  { name: 'Joe', age: 30, job: { title: 'Developer', language: 'JavaScript' } },
  //job 값이 없으면 undefined를 반환할 것입니다
  { name: 'Sarah', age: 35 }
]);
//job 안의 title프로퍼티를 뽑아냅니다
const example = source.pipe(pluck('job', 'title'));
//결과: "Developer" , undefined
const subscribe = example.subscribe(val => console.log(val));
```

### 관련된 사용법

* [Breakout Game](../../recipes/breakout-game.md)
* [Car Racing Game](../../recipes/car-racing-game.md)
* [Lockscreen](../../recipes/lockscreen.md)
* [Memory Game](../../recipes/memory-game.md)
* [Mine Sweeper Game](../../recipes/mine-sweeper-game.md)
* [Platform Jumper Game](../../recipes/platform-jumper-game.md)
* [Tetris Game](../../recipes/tetris-game.md)
* [Uncover Image Game](../../recipes/uncover-image-game.md)

### 추가 자료

* [pluck](https://rxjs.dev/api/operators/pluck) :newspaper: - 공식 문서

> :file\_folder: Source Code: [https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/pluck.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/pluck.ts)


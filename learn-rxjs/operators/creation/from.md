# from

#### signature: `from(ish: ObservableInput, mapFn: function, thisArg: any, scheduler: Scheduler): Observable`

## 배열, 프로미스, 이터러블을 옵저버블로 바꾼다.

:bulb: 이 연산자는 프로미스를 옵저버블로 바꿀때 사용될 수 있습니다!

:bulb: 배열과 이터러블의 경우, 포함된 모든 값들이 순차적으로 내보내집니다!

:bulb: 이 연산자는 또한 문자열을 순서대로 내보내는 데 사용될 수 있습니다!

### 예시

**예시 1: 배열에서의 옵저버블**

\( [StackBlitz](https://stackblitz.com/edit/typescript-sckwsw?file=index.ts&devtoolsheight=100) \| [jsBin](http://jsbin.com/foceyuketi/1/edit?js,console) \| [jsFiddle](https://jsfiddle.net/btroncone/o7kb5e6j/) \)

```javascript
// RxJS v6+
import { from } from 'rxjs';

//연속된 값으로 배열을 내보낸다
const arraySource = from([1, 2, 3, 4, 5]);
//결과: 1,2,3,4,5
const subscribe = arraySource.subscribe(val => console.log(val));
```

**예시 2: 프로미스에서의 옵저버블**

\( [StackBlitz](https://stackblitz.com/edit/typescript-clpg1f?file=index.ts&devtoolsheight=100) \| [jsBin](http://jsbin.com/tamofinujo/1/edit?js,console) \| [jsFiddle](https://jsfiddle.net/btroncone/2czc5sae/) \)

```javascript
// RxJS v6+
import { from } from 'rxjs';

//프로미스의 결과값을 내보낸다
const promiseSource = from(new Promise(resolve => resolve('Hello World!')));
//결과: 'Hello World'
const subscribe = promiseSource.subscribe(val => console.log(val));
```

**예시 3: 콜렉션에서의 옵저버블**

\( [StackBlitz](https://stackblitz.com/edit/typescript-drfckx?file=index.ts&devtoolsheight=100) \| [jsBin](http://jsbin.com/tezohobudu/1/edit?js,console) \| [jsFiddle](https://jsfiddle.net/btroncone/ae6hu9a8/) \)

```javascript
// RxJS v6+
import { from } from 'rxjs';

const map = new Map();
map.set(1, 'Hi');
map.set(2, 'Bye');

const mapSource = from(map);
//결과: [1, 'Hi'], [2, 'Bye']
const subscribe = mapSource.subscribe(val => console.log(val));
```

**예시 4: 문자열에서의 옵저버블**

\( [StackBlitz](https://stackblitz.com/edit/typescript-19nejh?file=index.ts&devtoolsheight=100) \| [jsBin](http://jsbin.com/wenozubana/1/edit?js,console) \| [jsFiddle](https://jsfiddle.net/btroncone/hfvzjcvL/) \)

```javascript
// RxJS v6+
import { from } from 'rxjs';

//문자열을 순서대로 내보낸다
const source = from('Hello World');
//결과: 'H','e','l','l','o',' ','W','o','r','l','d'
const subscribe = source.subscribe(val => console.log(val));
```

### 관련된 사용법

* [HTTP Polling](../../recipes/http-polling.md)
* [Lockscreen](../../recipes/lockscreen.md)
* [Memory Game](../../recipes/memory-game.md)
* [Progress Bar](../../recipes/progressbar.md)

### 추가 자료

* [from](https://rxjs.dev/api/index/function/from) :newspaper: - 공식 문서

* [Creation operators: from, fromArray, fromPromise](https://egghead.io/lessons/rxjs-creation-operators-from-fromarray-frompromise?course=rxjs-beyond-the-basics-creating-observables-from-scratch)

  :video\_camera: :dollar: - André Staltz

> :file\_folder: Source Code: [https://github.com/ReactiveX/rxjs/blob/master/src/internal/observable/from.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/observable/from.ts)


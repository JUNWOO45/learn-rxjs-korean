# filter

#### signature: `filter(select: Function, thisArg: any): Observable`

## 주어진 조건을 만족하는 값을 발생시킵니다.

💡 주어진 조건을 만족하지 않을 때 옵저버블을 종료시키기 원한다면, [takeWhile](takewhile.md) 을 살펴보세요!

### 예시

**예시 1: 짝수만 필터링합니다**

\( [StackBlitz](https://stackblitz.com/edit/typescript-4g4cys?file=index.ts&devtoolsheight=100) \| [jsBin](http://jsbin.com/vafogoluye/1/edit?js,console) \| [jsFiddle](https://jsfiddle.net/btroncone/tkz0fuy2/) \)

```javascript
// RxJS v6+
import { from } from 'rxjs';
import { filter } from 'rxjs/operators';

//(1,2,3,4,5)를 발생시킵니다
const source = from([1, 2, 3, 4, 5]);
//짝수가 아닌 수들을 걸러냅니다
const example = source.pipe(filter(num => num % 2 === 0));
//결과: "Even number: 2", "Even number: 4"
const subscribe = example.subscribe(val => console.log(`Even number: ${val}`));
```

**예시 2: 프로퍼티를 기준으로 객체 필터링**

\( [StackBlitz](https://stackblitz.com/edit/typescript-n73fsn?file=index.ts&devtoolsheight=100) \| [jsBin](http://jsbin.com/qihagaxuso/1/edit?js,console) \| [jsFiddle](https://jsfiddle.net/btroncone/yjdsoug1/) \)

```javascript
// RxJS v6+
import { from } from 'rxjs';
import { filter } from 'rxjs/operators';

//({name: 'Joe', age: 31}, {name: 'Bob', age:25}) 을 발생시킵니다
const source = from([{ name: 'Joe', age: 31 }, { name: 'Bob', age: 25 }]);
//age가 30 미만인 사람들을 걸러냅니다
const example = source.pipe(filter(person => person.age >= 30));
//결과: "Over 30: Joe"
const subscribe = example.subscribe(val => console.log(`Over 30: ${val.name}`));
```

**예시 3: 특정한 값보다 큰 수를 필터링합니다**

\( [StackBlitz](https://stackblitz.com/edit/typescript-eyvvfu?file=index.ts&devtoolsheight=100) \| [jsBin](http://jsbin.com/rakabaheyu/1/edit?js,console) \| [jsFiddle](https://jsfiddle.net/btroncone/g1tgreha/) \)

```javascript
// RxJS v6+
import { interval } from 'rxjs';
import { filter } from 'rxjs/operators';

//매 1초마다 값을 발생시킵니다
const source = interval(1000);
//interval로 발생시키는 값이 5보다 클 때까지, 모든 값들을 걸러냅니다
const example = source.pipe(filter(num => num > 5));
/*
  "Number greater than 5: 6"
  "Number greater than 5: 7"
  "Number greater than 5: 8"
  "Number greater than 5: 9"
*/
const subscribe = example.subscribe(val =>
  console.log(`Number greater than 5: ${val}`)
);
```

### 관련된 사용법

* [Battleship Game](../../recipes/battleship-game.md)
* [HTTP Polling](../../recipes/http-polling.md)
* [Game Loop](../../recipes/gameloop.md)
* [Lockscreen](../../recipes/lockscreen.md)
* [Mine Sweeper Game](../../recipes/mine-sweeper-game.md)
* \[Save Indicator\]\('../../recipes/save-indicator.md\)

### 추가 자료

* [filter](https://rxjs.dev/api/operators/filter) 📰 - 공식 문서
* [Adding conditional logic with filter](https://egghead.io/lessons/rxjs-adding-conditional-logic-with-filter?course=step-by-step-async-javascript-with-rxjs) 📹 💵 - John Linquist
* [Filtering operator: filter](https://egghead.io/lessons/rxjs-filtering-operator-filter?course=rxjs-beyond-the-basics-operators-in-depth) 📹 💵 - André Staltz
* [Build your own filter operator](https://blog.strongbrew.io/build-the-operators-from-rxjs-from-scratch/?lectureId=filter#app) 📹- Kwinten Pisman

> 📂 Source Code: [https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/filter.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/filter.ts)


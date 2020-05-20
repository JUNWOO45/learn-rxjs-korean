# partition

#### signature: `partition(predicate: function: boolean, thisArg: any): [Observable, Observable]`

## 하나의 옵저버블을 조건에 따라 나눕니다.

### 예시

**예시 1: 홀수, 짝수로 나눕니다.**

\( [StackBlitz](https://stackblitz.com/edit/typescript-gr3ljs?file=index.ts&devtoolsheight=100) \| [jsBin](http://jsbin.com/hipehexaku/1/edit?js,console) \| [jsFiddle](https://jsfiddle.net/btroncone/q0xo7gvv/) \)

```javascript
// RxJS v6+
import { from, merge } from 'rxjs';
import { partition, map } from 'rxjs/operators';

const source = from([1, 2, 3, 4, 5, 6]);
//true일 때는 첫번째 변수, false일 땐 두번째 변수에 담습니다.
const [evens, odds] = source.pipe(partition(val => val % 2 === 0));
/*
  결과:
  "Even: 2"
  "Even: 4"
  "Even: 6"
  "Odd: 1"
  "Odd: 3"
  "Odd: 5"
*/
const subscribe = merge(
  evens.pipe(map(val => `Even: ${val}`)),
  odds.pipe(map(val => `Odd: ${val}`))
).subscribe(val => console.log(val));
```

**예시 2: success과 error로 나눕니다.**

\( [StackBlitz](https://stackblitz.com/edit/typescript-vmfvp8?file=index.ts&devtoolsheight=100) \| [jsBin](http://jsbin.com/kukuguhuri/1/edit?js,console) \| [jsFiddle](https://jsfiddle.net/btroncone/fe246u5p/) \)

```javascript
// RxJS v6+
import { merge, of, from } from 'rxjs';
import { map, partition, catchError } from 'rxjs/operators';

const source = from([1, 2, 3, 4, 5, 6]);
// 3보다 크면 throw
const example = source.pipe(
  map(val => {
    if (val > 3) {
      throw `${val} greater than 3!`;
    }
    return { success: val };
  }),
  catchError(val => of({ error: val }))
);
//success 또는 error로 나누기
const [success, error] = example.pipe(partition(res => res.success));
/*
  결과:
  "Success! 1"
  "Success! 2"
  "Success! 3"
  "Error! 4 greater than 3!"
*/
const subscribe = merge(
  success.pipe(map(val => `Success! ${val.success}`)),
  error.pipe(map(val => `Error! ${val.error}`))
).subscribe(val => console.log(val));
```

**예시 3: \(v6.5+\) static function으로의 partition**

\( [StackBlitz](https://stackblitz.com/edit/typescript-vmfvp8?file=index.ts&devtoolsheight=100) \)

```javascript
// RxJS v6.5+
import { merge, of, from, partition } from 'rxjs';
import { map, catchError } from 'rxjs/operators';

const source = from([1, 2, 3, 4, 5, 6]);
// 3보다 크면 throw
const example = source.pipe(
  map(val => {
    if (val > 3) {
      throw `${val} greater than 3!`;
    }
    return { success: val };
  }),
  catchError(val => of({ error: val }))
);
// success 또는 error로 나누기
const [success, error] = partition(example, res => res.success);
/*
  결과:
  "Success! 1"
  "Success! 2"
  "Success! 3"
  "Error! 4 greater than 3!"
*/
const subscribe = merge(
  success.pipe(map(val => `Success! ${val.success}`)),
  error.pipe(map(val => `Error! ${val.error}`))
).subscribe(val => console.log(val));
```

### 추가 자료

* [partition](https://rxjs.dev/api/operators/partition) 📰 - 공식 문서

> 📂 Source Code: [https://github.com/ReactiveX/rxjs/blob/master/src/internal/observable/partition.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/observable/partition.ts)


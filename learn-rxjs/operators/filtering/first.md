# first

#### signature: `first(predicate: function, select: function)`

## 단순히 첫번째 값, 혹은 조건에 맞는 첫번째 값을 발생시킵니다

💡 first의 정반대는 [**last**](last.md) 입니다!

💡 만약 다음 통지가 전송되기 전에 옵저버블이 완료된다면, `First` 는 EmptyError를 옵저버의 콜백 에러에 전달합니다.이러한 동작을 원하지 않으면, `take(1)` 을 대신 사용하세요.

### 예시

\( [테스트 예시](https://github.com/btroncone/learn-rxjs/blob/master/operators/specs/filtering/first-spec.ts) \)

**예시 1: 연속된 값들 중 첫번째 값**

\( [StackBlitz](https://stackblitz.com/edit/typescript-t8hseq?file=index.ts&devtoolsheight=100) \| [jsBin](http://jsbin.com/kayenuxoma/1/edit?js,console) \| [jsFiddle](https://jsfiddle.net/btroncone/uncey4v9/) \)

```javascript
// RxJS v6+
import { from } from 'rxjs';
import { first } from 'rxjs/operators';

const source = from([1, 2, 3, 4, 5]);
//arguments가 없으면, 첫번째 값을 발생시킵니다
const example = source.pipe(first());
//결과: "First value: 1"
const subscribe = example.subscribe(val => console.log(`First value: ${val}`));
```

**예시 2: 조건을 만족하는 첫번째 값**

\( [StackBlitz](https://stackblitz.com/edit/typescript-bw5byu?file=index.ts&devtoolsheight=100) \| [jsBin](http://jsbin.com/pujowawovu/1/edit?js,console) \| [jsFiddle](https://jsfiddle.net/btroncone/pt36r8cu/) \)

```javascript
// RxJS v6+
import { from } from 'rxjs';
import { first } from 'rxjs/operators';

const source = from([1, 2, 3, 4, 5]);
//조건을 만족하는 첫번째 값을 발생시킵니다
const example = source.pipe(first(num => num === 5));
//결과: "First to pass test: 5"
const subscribe = example.subscribe(val =>
  console.log(`First to pass test: ${val}`)
);
```

**예시 3: 기본값 사용**

\( [StackBlitz](https://stackblitz.com/edit/typescript-2pkzpv?file=index.ts&devtoolsheight=100) \| [jsBin](http://jsbin.com/qoganeleqa/1/edit?js,console) \| [jsFiddle](https://jsfiddle.net/btroncone/owx2jdg1/3/) \)

```javascript
// RxJS v6+
import { from } from 'rxjs';
import { first } from 'rxjs/operators';

const source = from([1, 2, 3, 4, 5]);
//아무 값도 조건을 통과하지 못했으므로, 기본값을 발생시킵니다
const example = source.pipe(first(val => val > 5, 'Nothing'));
//결과: 'Nothing'
const subscribe = example.subscribe(val => console.log(val));
```

### 추가 자료

* [first](https://rxjs.dev/api/operators/first) 📰 - 공식 문서
* [Filtering operator: take, first, skip](https://egghead.io/lessons/rxjs-filtering-operators-take-first-skip?course=rxjs-beyond-the-basics-operators-in-depth) 📹 💵 - André Staltz

> 📂 Source Code: [https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/first.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/first.ts)


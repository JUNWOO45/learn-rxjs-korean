# single

#### signature: `single(a: Function): Observable`

## 조건을 만족하는 단 하나의 아이템을 발생시킵니다.

### 예시

**예시 1: 조건을 만족하는 하나의 아이템을 발생시킵니다**

\( [StackBlitz](https://stackblitz.com/edit/typescript-qhynlr?file=index.ts&devtoolsheight=100) \| [jsBin](http://jsbin.com/solecibuza/1/edit?js,console) \| [jsFiddle](https://jsfiddle.net/btroncone/26r5y90s/) \)

```javascript
// RxJS v6+
import { from } from 'rxjs';
import { single } from 'rxjs/operators';

// (1,2,3,4,5)를 발생시킵니다
const source = from([1, 2, 3, 4, 5]);
//조건을 만족하는 하나의 아이템을 발생시킵니다
const example = source.pipe(single(val => val === 4));
//결과: 4
const subscribe = example.subscribe(val => console.log(val));
```

### 추가 자료

* [single](https://rxjs.dev/api/operators/single) :newspaper: - 공식 문서


> :file\_folder: Source Code: [https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/single.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/single.ts)


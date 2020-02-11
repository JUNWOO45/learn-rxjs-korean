# ignoreElements

#### signature: `ignoreElements(): Observable`

## 완료와 에러를 제외한 모든 것들을 무시한다.

### 예시

**예시 1: 모든 것들을 무시합니다**

\( [StackBlitz](https://stackblitz.com/edit/typescript-jpjcpg?file=index.ts&devtoolsheight=100) \| [jsBin](http://jsbin.com/yiyefelubi/1/edit?js,console) \| [jsFiddle](https://jsfiddle.net/btroncone/59scjqss/) \)

```javascript
// RxJS v6+
import { interval } from 'rxjs';
import { take, ignoreElements } from 'rxjs/operators';

//매 100ms 간격으로 값을 내보냅니다
const source = interval(100);
//완료인 경우를 제외하고, 모든 값들을 무시합니다
const example = source.pipe(
  take(5),
  ignoreElements()
);
//결과: "COMPLETE!"
const subscribe = example.subscribe(
  val => console.log(`NEXT: ${val}`),
  val => console.log(`ERROR: ${val}`),
  () => console.log('COMPLETE!')
);
```

**예시 2: 에러만 내보냅니다**

\( [StackBlitz](https://stackblitz.com/edit/typescript-3yxv9z?file=index.ts&devtoolsheight=100) \| [jsBin](http://jsbin.com/gogonawuze/1/edit?js,console) \| [jsFiddle](https://jsfiddle.net/btroncone/srcwdgw6/) \)

```javascript
// RxJS v6+
import { interval, throwError, of } from 'rxjs';
import { mergeMap, ignoreElements } from 'rxjs/operators';

//매 100ms 간격으로 값을 내보냅니다
const source = interval(100);
//에러를 제외한 모든 것들을 무시합니다
const error = source.pipe(
  mergeMap(val => {
    if (val === 4) {
      return throwError(`ERROR AT ${val}`);
    }
    return of(val);
  }),
  ignoreElements()
);
//결과: "ERROR: ERROR AT 4"
const subscribe = error.subscribe(
  val => console.log(`NEXT: ${val}`),
  val => console.log(`ERROR: ${val}`),
  () => console.log('SECOND COMPLETE!')
);
```

### 추가 자료

* [ignoreElements](https://rxjs.dev/api/operators/ignoreElements)

  :newspaper: - 공식 문서

> :file\_folder: Source Code: [https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/ignoreElements.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/ignoreElements.ts)


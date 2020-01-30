# throw

#### signature: `throw(error: any, scheduler: Scheduler): Observable`

## subscription 시 에러를 내보냅니다.

### 예시

**예시 1: subscription시 에러를 내보냅니다.**

\( [StackBlitz](https://stackblitz.com/edit/typescript-5d3stz?file=index.ts&devtoolsheight=100) \| [jsBin](http://jsbin.com/punubequju/1/edit?js,console) \| [jsFiddle](https://jsfiddle.net/btroncone/mks82xqz/) \)

```javascript
// RxJS v6+
import { throwError } from 'rxjs';

//subscription시 정해진 값의 에러를 내보냅니다.
const source = throwError('This is an error!');
//결과: 'Error: This is an error!'
const subscribe = source.subscribe({
  next: val => console.log(val),
  complete: () => console.log('Complete!'),
  error: val => console.log(`Error: ${val}`)
});
```

### 관련된 사용법

* [Throwing after 3 retries](../error_handling/retrywhen.md)

### 추가 자료

* [throw](https://rxjs.dev/api/index/function/throw)

  :newspaper: - 공식 문서

* [Creation operators: empty, never, and throw](https://egghead.io/lessons/rxjs-creation-operators-empty-never-throw?course=rxjs-beyond-the-basics-creating-observables-from-scratch)

  :video\_camera: :dollar: - André Staltz

> :file\_folder: Source Code: [https://github.com/ReactiveX/rxjs/blob/master/src/internal/observable/throwError.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/observable/throwError.ts)


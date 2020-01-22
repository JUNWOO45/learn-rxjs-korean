# skipUntil

#### signature: `skipUntil(the: Observable): Observable`

## 제공된 옵저버블이 값을 발생할 때까지, 소스로부터 발생한 값을 건너뜁니다

### 예시

**예시 1: 옵저버블이 값을 발생시킬때까지 건너뜁니다**

\( [StackBlitz](https://stackblitz.com/edit/typescript-gs4mps?file=index.ts&devtoolsheight=100) \| [jsBin](http://jsbin.com/tapizososu/1/edit?js,console) \| [jsFiddle](https://jsfiddle.net/btroncone/xLu8nf77/) \)

```javascript
// RxJS v6+
import { interval, timer } from 'rxjs';
import { skipUntil } from 'rxjs/operators';

//매 1초마다 값을 발생
const source = interval(1000);
//내부 옵저버블로부터 값이 발생할 때까지(6s), 소스로부터 발생된 값을 건너뜁니다.
const example = source.pipe(skipUntil(timer(6000)));
//결과: 5...6...7...8........
const subscribe = example.subscribe(val => console.log(val));
```

### 추가 자료

* [skipUntil](https://rxjs.dev/api/operators/skipUntil)

  :newspaper: - 공식 문서

> :file\_folder: Source Code: [https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/skipUntil.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/skipUntil.ts)


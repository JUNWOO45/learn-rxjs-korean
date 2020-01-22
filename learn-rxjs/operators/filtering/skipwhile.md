# skipWhile

#### signature: `skipWhile(predicate: Function): Observable`

## 제공된 표현식이 거짓이 될 때까지, 발생한 값을 건너뜁니다.

### 예시

**예시1: 값이 참이면 건너뜁니다**

\( [StackBlitz](https://stackblitz.com/edit/typescript-p5kapz?file=index.ts&devtoolsheight=100) \| [jsBin](http://jsbin.com/bemikuleya/edit?js,console) \| [jsFiddle](https://jsfiddle.net/btroncone/3ymfxb09/) \)

```javascript
// RxJS v6+
import { interval } from 'rxjs';
import { skipWhile } from 'rxjs/operators';

//매 1초마다 값을 발생
const source = interval(1000);
//소스로부터 발생한 값이 5 미만이면 건너뜁니다
const example = source.pipe(skipWhile(val => val < 5));
//결과: 5...6...7...8........
const subscribe = example.subscribe(val => console.log(val));
```

### 추가 자료

* [skipWhile](https://rxjs.dev/api/operators/skipWhile)

  :newspaper: - 공식 문서

> :file\_folder: Source Code: [https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/skipWhile.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/skipWhile.ts)


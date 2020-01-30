# takeLast

#### signature: `takeLast(count: number): Observable`

## 마지막 n개의 값을 발생시키고 종료합니다

💡 여러개의 옵저버블에서 마지막으로 발생한 값만 필요하다면, 여러개의 옵저버블이 완료된 후 [forkJoin](../combination/forkjoin.md) 을 사용해보세요!

### 예시

**예시 1: 발생한 값 중 마지막 2개의 값만 가져오고 종료합니다**

\( [StackBlitz](https://stackblitz.com/edit/typescript-zss7oo?file=index.ts&devtoolsheight=100) \)

```javascript
// RxJS v6+
import { of } from 'rxjs';
import { takeLast } from 'rxjs/operators';

const source = of('Ignore', 'Ignore', 'Hello', 'World!');
// 마지막 2개의 발생한 값만 가져옵니다
const example = source.pipe(takeLast(2));
// Hello, World!
const subscribe = example.subscribe(val => console.log(val));
```

### 추가 자료

* [takeLast](https://rxjs-dev.firebaseapp.com/api/operators/takeLast) 📰 - 공식 문서

> 📂 Source Code: [https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/takeLast.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/takeLast.ts)


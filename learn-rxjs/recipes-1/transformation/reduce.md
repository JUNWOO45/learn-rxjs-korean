# reduce

#### signature: `reduce(accumulator: function, seed: any): Observable`

## 옵저버블의 값을 완료되었을 때 발생하는 단일값으로 감소시킵니다.

:bulb: [`Array.prototype.reduce()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce?v=a) 와 같습니다.

:bulb: 값이 발생할 때 마다, 현재 누적값이 필요한 경우엔 [scan](scan.md) 을 살펴보세요!

### 예시

**예시 1: 숫자 스트림의 합계**

\( [StackBlitz](https://stackblitz.com/edit/typescript-hdsv5e?file=index.ts&devtoolsheight=100) \| [jsBin](http://jsbin.com/dakuneneho/edit?js,console) \| [jsFiddle](https://jsfiddle.net/f8fw7yka/) \)

```javascript
// RxJS v6+
import { of } from 'rxjs';
import { reduce } from 'rxjs/operators';

const source = of(1, 2, 3, 4);
const example = source.pipe(reduce((acc, val) => acc + val));
//결과: Sum: 10'
const subscribe = example.subscribe(val => console.log('Sum:', val));
```

### 추가 자료

* [reduce](https://rxjs.dev/api/operators/reduce) :newspaper: - 공식 문서
* [Scan\(\) vs reduce\(\) \| RxJS TUTORIAL](https://www.youtube.com/watch?v=myEeo2rZc3g)

  :video\_camera: - Academind

* [Build your own reduce operator](https://blog.strongbrew.io/build-the-operators-from-rxjs-from-scratch/?lectureId=reduce#app)

  :video\_camera: - Kwinten Pisman

> :file\_folder: Source Code: [https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/reduce.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/reduce.ts)


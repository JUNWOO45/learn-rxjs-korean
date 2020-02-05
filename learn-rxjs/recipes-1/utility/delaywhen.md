# delayWhen

#### signature: `delayWhen(selector: Function, sequence: Observable): Observable`

## 주어진 함수의 조건만큼 기다린 후, 값을 내보냅니다

### 예시

**예시 1: 옵저버블 기반의 delayWhen**

\( [StackBlitz](https://stackblitz.com/edit/typescript-5yzn8g?file=index.ts&devtoolsheight=100) \| [jsBin](http://jsbin.com/topohekuje/edit?js,console) \| [jsFiddle](https://jsfiddle.net/btroncone/b057mxkL/) \)

```javascript
// RxJS v6+
import { interval, timer } from 'rxjs';
import { delayWhen } from 'rxjs/operators';

//매 초 마다 값을 내보냅니다.
const message = interval(1000);
//5초 뒤 값을 내보냅니다.
const delayForFiveSeconds = () => timer(5000);
//5초 뒤, 지연된 interval 값을 내보내기 시작합니다.
const delayWhenExample = message.pipe(delayWhen(delayForFiveSeconds));
//로그 값은 5초 동안 지연되었습니다.
//ex. 결과: 5s....1...2...3
const subscribe = delayWhenExample.subscribe(val => console.log(val));
```

### 추가 자료

* [delayWhen](https://rxjs.dev/api/operators/delayWhen) 📰 - 공식 문
* [Transformation operator: delay and delayWhen](https://egghead.io/lessons/rxjs-transformation-operators-delay-and-delaywhen?course=rxjs-beyond-the-basics-operators-in-depth) 📹 💵 - André Staltz

> 📂 Source Code: [https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/delayWhen.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/delayWhen.ts)


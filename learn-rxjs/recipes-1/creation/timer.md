# timer

#### signature: `timer(initialDelay: number | Date, period: number, scheduler: Scheduler): Observable`

## 주어진 시간이 지난 후, 지정된 시간간격마다 순서대로 숫자를 내보냅니다.

### 예시

**예시 1: 타이머가 하나의 값을 내보낸 후 완료합니다**

\( [StackBlitz](https://stackblitz.com/edit/typescript-fvkzgg?file=index.ts&devtoolsheight=100) \| [jsBin](http://jsbin.com/pazajanehu/1/edit?js,console) \| [jsFiddle](https://jsfiddle.net/btroncone/vpx0y8fu/) \)

```javascript
// RxJS v6+
import { timer } from 'rxjs';

// 두번째 인자가 없으므로, 1초의 시간이 흐른뒤 0을 내보낸 뒤 종료합니다.
const source = timer(1000);
//결과: 0
const subscribe = source.subscribe(val => console.log(val));
```

**예시 2: 1초의 시간이 흐른뒤, 매 2초마다 값을 내보냅니다.**

\( [StackBlitz](https://stackblitz.com/edit/typescript-h9pzxr?file=index.ts&devtoolsheight=100) \| [jsBin](http://jsbin.com/kejidofuje/1/edit?js,console) \| [jsFiddle](https://jsfiddle.net/btroncone/30ddov8j/) \)

```javascript
// RxJS v6+
import { timer } from 'rxjs';

/*
  타이머 연산자가 몇초 간격으로 값을 내보낼지를 정하는 두번째 인자를 받았으므로, 1초의 시간이 흐른뒤, 매 2초마다 값을 내보냅니다.
*/
const source = timer(1000, 2000);
//결과: 0,1,2,3,4,5......
const subscribe = source.subscribe(val => console.log(val));
```

### 관련된 사용법

* [HTTP Polling](../../recipes/http-polling.md)

### 추가 자료

* [timer](https://rxjs.dev/api/index/function/timer)

  :newspaper: - 공식 문서

* [Creation operators: interval and timer](https://egghead.io/lessons/rxjs-creation-operators-interval-and-timer?course=rxjs-beyond-the-basics-creating-observables-from-scratch)

  :video\_camera: :dollar: - André Staltz

* [Build your own timer operator](https://blog.strongbrew.io/build-the-operators-from-rxjs-from-scratch/?lectureId=timer#app)

  :video\_camera: - Kwinten Pisman

> :file\_folder: Source Code: [https://github.com/ReactiveX/rxjs/blob/master/src/internal/observable/timer.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/observable/timer.ts)


# mapTo

#### signature: `mapTo(value: any): Observable`

## 방출되는 값을 일정한 값으로 매핑합니다.

### 예시

**예시 1: 방출되는 값을 문자열로 매핑합니다.**

\( [StackBlitz](https://stackblitz.com/edit/typescript-fipd7a?file=index.ts&devtoolsheight=100) \| [jsBin](http://jsbin.com/qujolenili/1/edit?js,console) \| [jsFiddle](https://jsfiddle.net/btroncone/4ojq56ng/) \)

```javascript
// RxJS v6+
import { interval } from 'rxjs';
import { mapTo } from 'rxjs/operators';

//매 2초 마다 값을 방출시킵니다
const source = interval(2000);
//방출되는 값들을 하나의 값으로 매핑시킵니다.
const example = source.pipe(mapTo('HELLO WORLD!'));
//결과물: 'HELLO WORLD!'...'HELLO WORLD!'...'HELLO WORLD!'...
const subscribe = example.subscribe(val => console.log(val));
```

**예시 2: 클릭이벤트를 문자열로 매핑시킵니다.**

\( [StackBlitz](https://stackblitz.com/edit/typescript-btghci?file=index.ts&devtoolsheight=100) \| [jsBin](http://jsbin.com/xaheciwara/1/edit?js,console,output) \| [jsFiddle](https://jsfiddle.net/btroncone/52fqL4nn/) \)

```javascript
// RxJS v6+
import { fromEvent } from 'rxjs';
import { mapTo } from 'rxjs/operators';

//emit every click on document
//document에서 클릭이 발생할때마다 방출시킵니다.
const source = fromEvent(document, 'click');
//방출되는 값들을 하나의 값으로 매핑시킵니다.
const example = source.pipe(mapTo('GOODBYE WORLD!'));
//결과물: (클릭)'GOODBYE WORLD!'...
const subscribe = example.subscribe(val => console.log(val));
```

### 관련한 사용법

* [HTTP Polling](../../recipes/http-polling.md)
* \[Save Indicator\]\('../../recipes/save-indicator.md\)
* [Smart Counter](../../recipes/smartcounter.md)
* [Stop Watch](../../recipes/stop-watch.md)

### 추가 자료

* [mapTo](https://rxjs.dev/api/operators/mapTo) 📰 - 공식 문서
* [Changing behavior with mapTo](https://egghead.io/lessons/rxjs-changing-behavior-with-mapto?course=step-by-step-async-javascript-with-rxjs) 📹 💵 - John Linquist
* [Transformation operator: map and mapTo](https://egghead.io/lessons/rxjs-transformation-operator-map-and-mapto?course=rxjs-beyond-the-basics-operators-in-depth) 📹 💵 - André Staltz

> 📂 Source Code: [https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/mapTo.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/mapTo.ts)


# defer

#### signature: `defer(observableFactory: function(): SubscribableOrPromise): Observable`

## 주어진 subscription 함수로 옵저버블을 생성.

:bulb: [`defer`](https://github.com/ReactiveX/rxjs/blob/ecc73d2a1564d0d3edffba90eec76510e509236c/src/internal/observable/iif.ts#L94-L100) 는 [`iif`](../conditional/iif.md) 연산자의 일부로 사용된다!

### 예시

**예시 1: subscription 시점의 날짜/시간을 가져오기위해 지연**

\( [StackBlitz](https://stackblitz.com/edit/rxjs-defer-example?file=index.ts&devtoolsheight=100) \)

```javascript
// RxJS v6+
import { defer, of, timer, merge } from 'rxjs';
import { switchMap } from 'rxjs/operators';

const s1 = of(new Date()); //현재 date time을 잡아둔다
const s2 = defer(() => of(new Date())); //구독 시점의 date time을 잡아둔다

console.log(new Date());

timer(2000)
  .pipe(switchMap(_ => merge(s1, s2)))
  .subscribe(console.log);

/*
결과 => 
2019-02-10T12:38:30.000Z (현재 날짜/시간이 console log에 찍힘)
2019-02-10T12:38:30.000Z (s1의 날짜/시간이 console log에 찍힌다, 옵저버블이 생성된 시점의 날짜/시간이다.)
2019-02-10T12:38:32.000Z (s2의 날짜/시간이 console log에 찍힌다, subscription 시점의 날짜/시간이다.)
*/

/*//NOTE: '전통적인' js 의 코드로 위 코드를 구현해본다면:
setTimeout(() => {
  s1.subscribe(console.log);
  s2.subscribe(console.log);
}, 2000);
*/
```

### 관련한 사용법

* [Save Indicator](../../recipes/save-indicator.md)

### 추가 자료

* [defer](https://rxjs.dev/api/index/function/defer) :newspaper: - 공식 문서


> :file\_folder: Source Code: [https://github.com/ReactiveX/rxjs/blob/master/src/internal/observable/defer.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/observable/defer.ts)


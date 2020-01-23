# takeUntil

#### signature: `takeUntil(notifier: Observable): Observable`

## 넘겨받은 옵저버블이 값을 발생시킬 때까지 값을 발생시킵니다.

:bulb: 구체적인 갯수의 값이 필요하면, [take](take.md)를 살펴보세요!

### 예시

**예시 1: 타이머가 값을 발생시키기 전까지 값을 받습니다**

\( [StackBlitz](https://stackblitz.com/edit/typescript-ujwjbg?file=index.ts&devtoolsheight=100) \| [jsBin](http://jsbin.com/yevuhukeja/1/edit?js,console) \| [jsFiddle](https://jsfiddle.net/btroncone/zbe9dzb9/) \)

```javascript
// RxJS v6+
import { interval, timer } from 'rxjs';
import { takeUntil } from 'rxjs/operators';

//매 1초마다 값을 발생시킵니다
const source = interval(1000);
//5초 뒤, 값을 발생시킵니다
const timer$ = timer(5000);
//타이머가 5초 뒤 값을 발생시키면, 완료시킵니다
const example = source.pipe(takeUntil(timer$));
//결과: 0,1,2,3
const subscribe = example.subscribe(val => console.log(val));
```

**예시 2: 첫 5개의 짝수를 받습니다**

\( [StackBlitz](https://stackblitz.com/edit/typescript-djhv7s?file=index.ts&devtoolsheight=100) \| [jsBin](http://jsbin.com/doquqecara/1/edit?js,console) \| [jsFiddle](https://jsfiddle.net/btroncone/0dLeksLe/) \)

```javascript
// RxJS v6+
import { interval } from 'rxjs/observable/interval';
import { takeUntil, filter, scan, map, withLatestFrom } from 'rxjs/operators';

//매 1초마다 값을 발생시킵니다
const source = interval(1000);
//짝수 체크
const isEven = val => val % 2 === 0;
//짝수인 값만 받습니다
const evenSource = source.pipe(filter(isEven));
//짝수의 합을 구합니다
const evenNumberCount = evenSource.pipe(scan((acc, _) => acc + 1, 0));
//5개의 짝수가 값을 발생시키기 전까진, 값을 발생시키지 않습니다
const fiveEvenNumbers = evenNumberCount.pipe(filter(val => val > 5));

const example = evenSource.pipe(
  //현재 짝수의 갯수를 출력합니다
  withLatestFrom(evenNumberCount),
  map(([val, count]) => `Even number (${count}) : ${val}`),
  //5개의 짝수가 발생되어지면, 옵저버블을 종료시킵니다
  takeUntil(fiveEvenNumbers)
);
/*
    Even number (1) : 0,
  Even number (2) : 2
    Even number (3) : 4
    Even number (4) : 6
    Even number (5) : 8
*/
const subscribe = example.subscribe(val => console.log(val));
```

**예시 3: 마우스가 올라갈 때까지, 마우스가 내려가는 마우스 이벤트를 받습니다**

\( [StackBlitz](https://stackblitz.com/edit/rxjs-ug2ezf?file=index.ts&devtoolsheight=50) \)

```javascript
// RxJS v6+
import { fromEvent } from 'rxjs';
import { takeUntil, mergeMap, map } from 'rxjs/operators';

const mousedown$ = fromEvent(document, 'mousedown');
const mouseup$ = fromEvent(document, 'mouseup');
const mousemove$ = fromEvent(document, 'mousemove');

// 마우스가 아래로 내려가면, 마우스가 다시 올라갈 때까지 위치정보를 받습니다
mousedown$
  .pipe(
    mergeMap(_ => {
      return mousemove$.pipe(
        map((e: any) => ({
          x: e.clientX,
          y: e.clientY
        })),
        // mouseup 이벤트에대해 내부 옵저버블을 완료합니다
        takeUntil(mouseup$)
      );
    })
  )
  .subscribe(console.log);
```

### 관련 사용법

* [Lockscreen](../../recipes/lockscreen.md)
* [Space Invaders Game](../../recipes/space-invaders-game.md)
* [Swipe To Refresh](../../recipes/swipe-to-refresh.md)

### 추가 자료

* [takeUntil](https://rxjs.dev/api/operators/takeUntil) :newspaper: - 공식 문서
* [Avoiding takeUntil leaks](https://blog.angularindepth.com/rxjs-avoiding-takeuntil-leaks-fb5182d047ef) - Angular in Depth
* [Stopping a stream with takeUntil](https://egghead.io/lessons/rxjs-stopping-a-stream-with-takeuntil?course=step-by-step-async-javascript-with-rxjs) :video\_camera: :dollar: - John Linquist
* [Build your own takeUntil operator](https://blog.strongbrew.io/build-the-operators-from-rxjs-from-scratch/?lectureId=takeUntil#app) :video\_camera: - Kwinten Pisman

> :file\_folder: Source Code: [https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/takeUntil.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/takeUntil.ts)


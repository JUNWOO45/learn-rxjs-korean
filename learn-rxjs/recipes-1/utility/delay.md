# delay

#### signature: `delay(delay: number | Date, scheduler: Scheduler): Observable`

## 주어진 시간만큼 기다린 후 값을 내보냅니다.

### 예시

**예시 1: 마우스를 길게 누르는것을 인식할 때까지 기다립니다**

\( [StackBlitz](https://stackblitz.com/edit/rxjs-bru5fi?devtoolsheight=60) \)

```javascript
import { fromEvent, of } from 'rxjs';
import { mergeMap, delay, takeUntil } from 'rxjs/operators';

const mousedown$ = fromEvent(document, 'mousedown');
const mouseup$ = fromEvent(document, 'mouseup');

mousedown$
  .pipe(
    mergeMap(event =>
      of(event).pipe(
        delay(700),
        takeUntil(mouseup$)
      )
    )
  )
  .subscribe(event => console.log('Long Press!', event));
```

**예시 2: Delay for increasing durations**

\( [StackBlitz](https://stackblitz.com/edit/typescript-twjn8r?file=index.ts&devtoolsheight=100) \)

```javascript
// RxJS v6+
import { of, merge } from 'rxjs';
import { mapTo, delay } from 'rxjs/operators';

//아이템 하나를 내보냅니다
const example = of(null);
//각각의 결과값을 추가 시간만큼 늦춥니다
const message = merge(
  example.pipe(mapTo('Hello')),
  example.pipe(
    mapTo('World!'),
    delay(1000)
  ),
  example.pipe(
    mapTo('Goodbye'),
    delay(2000)
  ),
  example.pipe(
    mapTo('World!'),
    delay(3000)
  )
);
//결과: 'Hello'...'World!'...'Goodbye'...'World!'
const subscribe = message.subscribe(val => console.log(val));
```

### 관련된 사용법

* [Battleship Game](../../recipes/battleship-game.md)
* [Progress Bar](../../recipes/progressbar.md)
* \[Save Indicator\]\('../../recipes/save-indicator.md\)
* [Swipe To Refresh](../../recipes/swipe-to-refresh.md)

### 추가 자료

* [delay](https://rxjs.dev/api/operators/delay) :newspaper: - 공식 문서
* [Transformation operator: delay and delayWhen](https://egghead.io/lessons/rxjs-transformation-operators-delay-and-delaywhen?course=rxjs-beyond-the-basics-operators-in-depth)

  :video\_camera: :dollar: - André Staltz

> :file\_folder: Source Code: [https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/delay.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/delay.ts)


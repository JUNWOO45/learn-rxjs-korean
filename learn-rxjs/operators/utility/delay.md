# delay

#### signature: `delay(delay: number | Date, scheduler: Scheduler): Observable`

## Delay emitted values by given time.

### Examples

**Example 1: Delay to recognize long press**

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

**Example 2: Delay for increasing durations**

\( [StackBlitz](https://stackblitz.com/edit/typescript-twjn8r?file=index.ts&devtoolsheight=100) \)

```javascript
// RxJS v6+
import { of, merge } from 'rxjs';
import { mapTo, delay } from 'rxjs/operators';

//emit one item
const example = of(null);
//delay output of each by an extra second
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
//output: 'Hello'...'World!'...'Goodbye'...'World!'
const subscribe = message.subscribe(val => console.log(val));
```

### Related Recipes

* [Battleship Game](../../recipes/battleship-game.md)
* [Progress Bar](../../recipes/progressbar.md)
* \[Save Indicator\]\('../../recipes/save-indicator.md\)
* [Swipe To Refresh](../../recipes/swipe-to-refresh.md)

### Additional Resources

* [delay](https://rxjs.dev/api/operators/delay) :newspaper: - Official docs
* [Transformation operator: delay and delayWhen](https://egghead.io/lessons/rxjs-transformation-operators-delay-and-delaywhen?course=rxjs-beyond-the-basics-operators-in-depth)

  :video\_camera: :dollar: - André Staltz

> :file\_folder: Source Code: [https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/delay.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/delay.ts)


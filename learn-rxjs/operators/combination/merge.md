# merge

#### signature: `merge(input: Observable): Observable`

## Turn multiple observables into a single observable.

:bulb: This operator can be used as either a static or instance method!

:bulb: If order not throughput is a primary concern, try [concat](concat.md) instead!

### Examples

**Example 1: merging multiple observables, static method**

\( [StackBlitz](https://stackblitz.com/edit/typescript-ohq6rx?file=index.ts&devtoolsheight=100) \| [jsBin](http://jsbin.com/conufujapi/1/edit?js,console) \| [jsFiddle](https://jsfiddle.net/btroncone/qvq9dscu/) \)

```javascript
// RxJS v6+
import { mapTo } from 'rxjs/operators';
import { interval, merge } from 'rxjs';

//emit every 2.5 seconds
const first = interval(2500);
//emit every 2 seconds
const second = interval(2000);
//emit every 1.5 seconds
const third = interval(1500);
//emit every 1 second
const fourth = interval(1000);

//emit outputs from one observable
const example = merge(
  first.pipe(mapTo('FIRST!')),
  second.pipe(mapTo('SECOND!')),
  third.pipe(mapTo('THIRD')),
  fourth.pipe(mapTo('FOURTH'))
);
//output: "FOURTH", "THIRD", "SECOND!", "FOURTH", "FIRST!", "THIRD", "FOURTH"
const subscribe = example.subscribe(val => console.log(val));
```

**Example 2: merge 2 observables, instance method**

\( [StackBlitz](https://stackblitz.com/edit/typescript-bcsl1r?file=index.ts&devtoolsheight=100) \| [jsBin](http://jsbin.com/wuwujokaqu/1/edit?js,console) \| [jsFiddle](https://jsfiddle.net/btroncone/me5ofcr0/) \)

```javascript
// RxJS v6+
import { merge } from 'rxjs/operators';
import { interval } from 'rxjs';

//emit every 2.5 seconds
const first = interval(2500);
//emit every 1 second
const second = interval(1000);
//used as instance method
const example = first.pipe(merge(second));
//output: 0,1,0,2....
const subscribe = example.subscribe(val => console.log(val));
```

### Related Recipes

* [Battleship Game](../../recipes/battleship-game.md)
* [Flappy Bird Game](../../recipes/flappy-bird-game.md)
* [HTTP Polling](../../recipes/http-polling.md)
* [Lockscreen](../../recipes/lockscreen.md)
* [Memory Game](../../recipes/memory-game.md)
* \[Save Indicator\]\('../../recipes/save-indicator.md\)

### Additional Resources

* [merge](https://rxjs.dev/api/index/function/merge)

  :newspaper: - Official docs

* [Handling multiple streams with merge](https://egghead.io/lessons/rxjs-handling-multiple-streams-with-merge?course=step-by-step-async-javascript-with-rxjs)

  :video\_camera: :dollar: - John Linquist

* [Sharing network requests with merge](https://egghead.io/lessons/rxjs-reactive-programming-sharing-network-requests-with-rxjs-merge?course=introduction-to-reactive-programming)

  :video\_camera: :dollar: - André Staltz

* [Combination operator: merge](https://egghead.io/lessons/rxjs-combination-operator-merge?course=rxjs-beyond-the-basics-operators-in-depth)

  :video\_camera: :dollar: - André Staltz

* [Build your own merge operator](https://blog.strongbrew.io/build-the-operators-from-rxjs-from-scratch/?lectureId=merge#app)

  :video\_camera: - Kwinten Pisman

> :file\_folder: Source Code: [https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/merge.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/merge.ts)

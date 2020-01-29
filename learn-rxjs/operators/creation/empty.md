# empty

#### signature: `empty(scheduler: Scheduler): Observable`

## 즉시 완료되는 옵저버블.

### 예시

**예시 1: empty 는 즉시 완료시킨다**

\( [StackBlitz](https://stackblitz.com/edit/typescript-aqfpkq?file=index.ts&devtoolsheight=100) \| [jsBin](http://jsbin.com/rodubucaqa/1/edit?js,console) \| [jsFiddle](https://jsfiddle.net/btroncone/bz71mzuy/) \)

```javascript
// RxJS v6+
import { empty } from 'rxjs';

//결과: 'Complete!'
const subscribe = empty().subscribe({
  next: () => console.log('Next'),
  complete: () => console.log('Complete!')
});
```

**예시 2: 타이머를 사용하는 empty**

\( [StackBlitz](https://stackblitz.com/edit/typescript-uujo8t?file=index.ts&devtoolsheight=50) \)

```javascript
// RxJS v6+
import { interval, fromEvent, merge, empty } from 'rxjs';
import { switchMap, scan, takeWhile, startWith, mapTo } from 'rxjs/operators';

const countdownSeconds = 10;
const setHTML = id => val => (document.getElementById(id).innerHTML = val);
const pauseButton = document.getElementById('pause');
const resumeButton = document.getElementById('resume');
const interval$ = interval(1000).pipe(mapTo(-1));

const pause$ = fromEvent(pauseButton, 'click').pipe(mapTo(false));
const resume$ = fromEvent(resumeButton, 'click').pipe(mapTo(true));

const timer$ = merge(pause$, resume$)
  .pipe(
    startWith(true),
    // 타이머가 멈추면, 빈 옵저버블을 반환한다
    switchMap(val => (val ? interval$ : empty())),
    scan((acc, curr) => (curr ? curr + acc : acc), countdownSeconds),
    takeWhile(v => v >= 0)
  )
  .subscribe(setHTML('remaining'));
```

### 관련한 사용법

* [Memory Game](../../recipes/memory-game.md)
* [Save Indicator](../../recipes/save-indicator.md)

### 추가 자료

* [empty](https://rxjs.dev/api/index/function/empty) 📰 - 공식 문서
* [Creation operators: empty, never, and throw](https://egghead.io/lessons/rxjs-creation-operators-empty-never-throw?course=rxjs-beyond-the-basics-creating-observables-from-scratch) 📹 💵 - André Staltz

> 📂 Source Code: [https://github.com/ReactiveX/rxjs/blob/master/src/internal/observable/EmptyObservable.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/observable/EmptyObservable.ts)


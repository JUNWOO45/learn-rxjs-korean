# generate

#### signature: `generate(initialStateOrOptions: GenerateOptions, condition?: ConditionFunc, iterate?: IterateFunc, resultSelectorOrObservable?: (ResultFunc) | SchedulerLike, scheduler?: SchedulerLike): Observable`

## 지정된 스케줄러를 사용하여 반복문을 실행하여 옵저버블을 만들어냅니다.

### 예시

**예시 1: 옵저버블 만들어내기**

\( [StackBlitz](https://stackblitz.com/edit/rxjs-generate?file=index.ts&devtoolsheight=100) \)

```javascript
// RxJS v6+
import { generate } from 'rxjs';

generate(2, x => x <= 8, x => x + 3).subscribe(console.log);

/*
결과:
2
5
8
*/
```

**예시 2: result selector를 사용해서 옵저버블 만들어내기**

\( [StackBlitz](https://stackblitz.com/edit/rxjs-generate-result-selector?file=index.ts&devtoolsheight=100) \)

```javascript
// RxJS v6+
import { generate } from 'rxjs';

generate(2, x => x <= 38, x => x + 3, x => '.'.repeat(x)).subscribe(
  console.log
);

/*
결과:
..
.....
........
...........
..............
.................
....................
.......................
..........................
.............................
................................
...................................
......................................
*/
```

### 관련된 사용법

* [Breakout Game](../../recipes/breakout-game.md)
* [Memory Game](../../recipes/memory-game.md)

### 추가 자료

* [generate](https://rxjs.dev/api/index/function/generate)

  :newspaper: - 공식 문서

> :file\_folder: Source Code: [https://github.com/ReactiveX/rxjs/blob/master/src/internal/observable/generate.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/observable/generate.ts)


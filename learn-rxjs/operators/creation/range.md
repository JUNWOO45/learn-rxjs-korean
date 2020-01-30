# range

#### signature: `range(start: number, count: number, scheduler: Scheduler): Observable`

## 주어진 범위의 숫자를 순서대로 내보냅니다.

### 예시

**예시 1: 1-10의 숫자를 내보냅니다.**

\( [StackBlitz](https://stackblitz.com/edit/typescript-r5zrww?file=index.ts&devtoolsheight=100) \| [jsBin](http://jsbin.com/yalefomage/1/edit?js,console) \| [jsFiddle](https://jsfiddle.net/btroncone/cfvfgwn9/) \)

```javascript
// RxJS v6+
import { range } from 'rxjs';

// 1-10을 순서대로 내보냅니다.
const source = range(1, 10);
//결과: 1,2,3,4,5,6,7,8,9,10
const example = source.subscribe(val => console.log(val));
```

### 추가 자료

* [range](https://rxjs.dev/api/index/function/range)

  :newspaper: - 공식 문서

> :file\_folder: Source Code: [https://github.com/ReactiveX/rxjs/blob/master/src/internal/observable/range.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/observable/range.ts)


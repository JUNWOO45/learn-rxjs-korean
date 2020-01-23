# distinct

#### signature: `distinct(keySelector?, flushes?): Observable`

## 이전에 발생하지 않았던 아이템을 발생시킵니다.

### 예시

**예시 1: 선택자 없이 구분하기**

\( [StackBlitz](https://stackblitz.com/edit/rxjs-distinct-example-wphfch?file=index.ts&devtoolsheight=100) \)

```javascript
// RxJS v6+
import { of } from 'rxjs';
import { distinct } from 'rxjs/operators';

of(1, 2, 3, 4, 5, 1, 2, 3, 4, 5)
  .pipe(distinct())
  // 결과: 1,2,3,4,5
  .subscribe(console.log);
```

**예시 2: key값으로 구분하기**

\( [StackBlitz](https://stackblitz.com/edit/rxjs-distinct-example?file=index.ts&devtoolsheight=100) \)

```javascript
// RxJS v6+
import { from } from 'rxjs';
import { distinct } from 'rxjs/operators';

const obj1 = { id: 3, name: 'name 1' };
const obj2 = { id: 4, name: 'name 2' };
const obj3 = { id: 3, name: 'name 3' };
const vals = [obj1, obj2, obj3];

from(vals)
  .pipe(distinct(e => e.id))
  .subscribe(console.log);

/*
OUTPUT:
{id: 3, name: "name 1"}
{id: 4, name: "name 2"}
 */
```

### 추가 자료

* [distinct](https://rxjs.dev/api/operators/distinct) :newspaper: - 공식 문서


> :file\_folder: Source Code: [https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/distinct.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/distinct.ts)


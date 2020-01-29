# find

#### signature: `find(predicate: function)`

## 조건을 만족하는 첫번째 아이템을 발생시킨 이후, 완료합니다.

💡 조건과 상과없이 항상 첫번째 아이템을 발생시키길 원한다면, [`first()`](first.md) 를 확인해보세요!

### 예시

**예시 1: 박스 내부를 클릭하면 성공, 박스 외부를 클릭하면 계속 반복**

\( [StackBlitz](https://stackblitz.com/edit/rxjs-hd63we?file=index.ts)\)

```javascript
// RxJS v6+
import { fromEvent } from 'rxjs';
import { find, repeatWhen, mapTo, startWith, filter } from 'rxjs/operators';

// 엘리먼트 참조
const status = document.getElementById('status');

// 스트림
const clicks$ = fromEvent(document, 'click');

clicks$
  .pipe(
    find((event: any) => event.target.id === 'box'),
    mapTo('Found!'),
    startWith('Find me!'),
    // 박스 외부를 클릭하면 초기화합니다
    repeatWhen(() =>
      clicks$.pipe(filter((event: any) => event.target.id !== 'box'))
    )
  )
  .subscribe(message => (status.innerHTML = message));
```

### 추가 자료

* [find](https://rxjs.dev/api/operators/find) 📰 - 공식 문서

> 📂 Source Code: [https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/find.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/find.ts)


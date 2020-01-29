# skip

#### signature: `skip(the: Number): Observable`

## 제공된 수 만큼, 발생된 값을 건너뜁니다

### 왜 `skip` 을 사용할까요?

Skip은 소스로부터 발생된 값들 중 순서대로 x개 만큼을 무시할 수 있게 해줍니다. `skip` 은 보통, subscription에 여러분이 항상 무시하고자하는 특정 값을 발생시키는 옵저버블이 있을때 사용됩니다. 아마 그러한 값들 중 몇몇개는 필요가 없는 값들이거나 `Replay` 혹은 `BehaviorSubject` 를 subscribing하고 있을 것입니다. 뒤늦게 발생하는 값들이 중요하다면, `skip` 을 사용해서 건너뛰세요.

index가 있는 [`filter`](filter.md) 를 사용해서 `skip` 의 동작을 만들어낼 수도 있습니다. 예시: `.filter((val, index) => index > 1)`

### 예시

**예시 1: 발생 전에 값 건너뛰기**

\( [StackBlitz](https://stackblitz.com/edit/typescript-o5ydjf?file=index.ts&devtoolsheight=100) \| [jsBin](http://jsbin.com/hacepudabi/1/edit?js,console) \| [jsFiddle](https://jsfiddle.net/btroncone/ar1eqbya/) \)

```javascript
// RxJS v6+
import { interval } from 'rxjs';
import { skip } from 'rxjs/operators';

//매 1초마다 값 발생
const source = interval(1000);
//첫 5개의 발생된 값 건너뛰기
const example = source.pipe(skip(5));
//결과: 5...6...7...8........
const subscribe = example.subscribe(val => console.log(val));
```

#### 예시2: 특정 filter 사용사례에 대한 짧은 설명

\( [StackBlitz](https://stackblitz.com/edit/typescript-yl3ap1?file=index.ts&devtoolsheight=100) \| [jsBin](http://jsbin.com/judamurego/edit?js,console) \| [jsFiddle](https://jsfiddle.net/ElHuy/4jswLn3z/) \)

```javascript
// RxJS v6+
import { from } from 'rxjs';
import { skip, filter } from 'rxjs/operators';

const numArrayObs = from([1, 2, 3, 4, 5, 6, 7, 8, 9, 10]);

// 3,4,5...
const skipObs = numArrayObs.pipe(skip(2)).subscribe(console.log);

// 3,4,5...
const filterObs = numArrayObs
  .pipe(filter((val, index) => index > 1))
  .subscribe(console.log);

//같은 결과군요!
```

### 추가 자료

* [skip](https://rxjs.dev/api/operators/skip) 📰 - 공식 문서
* [Filtering 연산자: take, first, skip](https://egghead.io/lessons/rxjs-filtering-operators-take-first-skip?course=rxjs-beyond-the-basics-operators-in-depth) 📹💵 - André Staltz

> 📂 소스 코드: [https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/skip.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/skip.ts)


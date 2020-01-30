# take

#### signature: `take(count: number): Observable`

## 제공된 수 만큼의 값만 발생시키고 종료합니다.

### 왜 `take` 를 사용할까요?

만약 여러분이 첫번째로 발생한 값만을 원한다면, `take` 를 사용하세요. 여러분은 사용자가 페이지에 들어와서 처음 클릭한 내용을 확인하거나, 클릭 이벤트를 구독한 뒤 가장 처음 발생한 값만을 보고싶을 수 있습니다. 또 다른 사례는 특정 시점에서 데이터 스냅샷을 작성해야 하지만, 이후 추가적인 값 발생은 원하지 않는 경우입니다. 예를 들어, 사용자 토큰 업데이트의 스트림이나, 앵귤러 애플리케이션에서의 라우트 가드 기반의 스트림이 있습니다.

💡 만약 여러분이 특정 로직이나, 다른 옵저버블을 기반으로 여러 값들을 받고싶다면, [takeUntil](takeuntil.md) 이나 [takeWhile](takewhile.md) 를 확인해보세요!

💡 `take` 는 첫 n개의 값만 발생시키는 반면, 정반대인 [`skip`](skip.md) 은 첫 n개의 값을 건너뛰고 값을 발생시킵니다.

### 예시

**예시 1: 소스로부터 1개의 값만 받기**

\( [StackBlitz](https://stackblitz.com/edit/typescript-uk92ax?file=index.ts&devtoolsheight=100) \| [jsBin](http://jsbin.com/vaxitupiwi/1/edit?js,console) \| [jsFiddle](https://jsfiddle.net/btroncone/f9bz0tr3/) \)

```javascript
// RxJS v6+
import { of } from 'rxjs';
import { take } from 'rxjs/operators';

//1,2,3,4,5를 발생시킵니다
const source = of(1, 2, 3, 4, 5);
//발생된 값 중 첫번째 값만 받고 종료시킵니다.
const example = source.pipe(take(1));
//결과: 1
const subscribe = example.subscribe(val => console.log(val));
```

**예시 2: 소스로부터 첫 5개의 값만 받기**

\( [StackBlitz](https://stackblitz.com/edit/typescript-3ujuth?file=index.ts&devtoolsheight=100) \| [jsBin](http://jsbin.com/kexenuzulu/edit?js,console) \| [jsFiddle](https://jsfiddle.net/btroncone/g1fhxgua/) \)

```javascript
// RxJS v6+
import { interval } from 'rxjs';
import { take } from 'rxjs/operators';

//매 1초마다 값을 발생시킵니다
const interval$ = interval(1000);
//발생된 값 중 첫 5개의 값만 받습니다
const example = interval$.pipe(take(5));
//결과: 0,1,2,3,4
const subscribe = example.subscribe(val => console.log(val));
```

**예시 3: 첫번째 클릭 위치를 받기**

\([StackBlitz](https://stackblitz.com/edit/typescript-8g9xt5?file=index.ts&devtoolsheight=50) \| [jsFiddle](https://jsfiddle.net/ElHuy/9c5j064x/)\)

```markup
<div id="locationDisplay">
  Where would you click first?
</div>
```

```javascript
// RxJS v6+
import { fromEvent } from 'rxjs';
import { take, tap } from 'rxjs/operators';

const oneClickEvent = fromEvent(document, 'click').pipe(
  take(1),
  tap(v => {
    document.getElementById(
      'locationDisplay'
    ).innerHTML = `Your first click was on location ${v.screenX}:${v.screenY}`;
  })
);

const subscribe = oneClickEvent.subscribe();
```

### 관련 사용법

* [Battleship Game](../../recipes/battleship-game.md)
* [Memory Game](../../recipes/memory-game.md)

### 추가 자료

* [take](https://rxjs.dev/api/operators/take) 📰 - 공식 문서
* [Filtering operator: take, first, skip](https://egghead.io/lessons/rxjs-filtering-operators-take-first-skip?course=rxjs-beyond-the-basics-operators-in-depth) 📹 💵 - André Staltz
* [Build your own take operator](https://blog.strongbrew.io/build-the-operators-from-rxjs-from-scratch/?lectureId=take#app) 📹- Kwinten Pisman

> 📂 Source Code: [https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/take.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/take.ts)


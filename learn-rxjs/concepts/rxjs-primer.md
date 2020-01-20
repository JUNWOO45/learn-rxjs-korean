# RxJS 입문서

RxJS를 처음 접하시나요? 이 페이지에서는 RxJS를 이해하는데 필요한 모든 주요 개념들을 배우고, RxJS를 다뤄볼 것입니다. 준비되었으면 시작해봅시다!

## Observable이란?

옵저버블은 시간의 흐름에 따라 도착하는 스트림, 또는 데이터의 출처를 의미합니다. 우린 거의 대부분의 것들에서 옵저버블을 만들어낼 수 있지만, 이벤트에서 사용되어지는 일이 가장 흔합니다. 이벤트는 마우스의 움직임, 버튼 클릭,텍스트 필드를 채워넣는 행위, 라우트 변경 등을 의미합니다. 옵저버블을 생성하는 가장 쉬운 방법은 내장된 생성 함수를 사용하는 것입니다. 예를 들어, 마우스 클릭 이벤트의 옵저버블을 만들기 위해 [`fromEvent`](../operators/creation/fromevent.md) 함수를 사용할 수 있습니다:

```javascript
// fromEvent 연산자를 가져옵니다
import { fromEvent } from 'rxjs';

// button을 참조
const button = document.getElementById('myButton');

// 버튼 클릭 옵저버블을 생성합니다
const myObservable = fromEvent(button, 'click');
```

이 시점에서 우린 옵저버블을 가지고 있지만, 옵저버블은 아무 행동도 하지 않습니다. **왜냐하면 옵저버블이 cold하거나, Subscription이 있기 전까지는 활성화되지 않기 때문입니다.**

## Subscription

Subscriptions은 모든 것을 동작하게 합니다. 이걸 수도꼭지에 비유할 수 있는데, 누군가가 손잡이를 돌리기만 하면 물줄기(옵저버블)가 흐르거나 멈출 수 있습니다. `subscriber` 가 이러한 역할을 합니다.

subscription을 만들기 위해서는, `observer` 라고 부르는 함수와 함께 `subscribe` 메소드를 호출해야 합니다. 이 곳에서 각각의 이벤트에대해 어떻게 행동할지 결정할 수 있습니다. Subscription이 생성될 때, 이전 시나리오에서 무슨 일이 일어나는지 확인해봅시다:

```javascript
// fromEvent 연산자를 가져옵니다
import { fromEvent } from 'rxjs';

// button을 참조
const button = document.getElementById('myButton');

// 버튼 클릭 옵저버블을 생성합니다
const myObservable = fromEvent(button, 'click');

// 자, 이젠 클릭할 때 마다 로그를 생성합니다
const subscription = myObservable.subscribe(event => console.log(event));
```

위 예시에서,myObservable.subscribe()` 은 다음과 같은 일을 합니다:

1. 버튼에 클릭 이벤트에 대한 이벤트 리스너를 설정합니다.
2. 매 클릭 이벤트 마다 subscribe 메소드와 함께 넘겨준 함수 \(observer\) 를 실행합니다.

3. 적절한 이벤트 리스너 삭제와 같은 일을 하는 `unsubscribe` 와 함께  Subscription 객체를 반환합니다.


Subscribe 메소드는 에러나 완료 처리를 다루기 위해 object map 또한 허용합니다. 이 기능을 자주 사용하지 않을테지만, 다음과 같이 필요한 경우가 있을 수 있어 알고있는 것이 좋습니다:

```javascript
// 함수 대신, next, error, 그리고 complete 객체를 넘겨줍니다
const subscription = myObservable.subscribe({
  // 이벤트 발생이 성공하면,
  next: event => console.log(event),
  // 에러,
  error: error => console.log(error),
  // 완료되면,
  complete: () => console.log('complete!')
});
```

각각의 subscription이 새로운 실행 컨텍스트를 생성한다는 점이 중요합니다. 즉, 2번째 호출한 `subscribe` 는 새로운 이벤트 리스너를 만듭니다.

```javascript
// 첫번째
const subscription = myObservable.subscribe(event => console.log(event));

// 두번째
const secondSubscription = myObservable.subscribe(event => console.log(event));

// unsubscribe를 사용해서 삭제
subscription.unsubscribe();
secondSubscription.unsubscribe();
```

기본적으로, Subscription은 옵저버블과 옵저버사이의 1대1이면서도 일방적인 데이터흐름을 만들어냅니다. 마치 여러분의 상사(옵저버블)가 구린 PR을 머지했다고 당신(옵저버)에게 소리치는 것(방출)과 비슷합니다. 바로 **unicasting** 으로 알려져있는 방법이죠. 만약 당신이 컨퍼런스 대화를 좋아한다면 - 한 명의 옵저버블과 수많은 옵저버들 - 당신은 **multicasting** 을 포함하는 다른 방법을 취해야 할 것입니다. 이와 관련해서는 나중에 더 알아보죠!

옵저버에게 데이터를 방출하는 옵저버블은, push 기반의 모델이라는 점을 유의해야합니다. Subscriber가 이 데이터로 뭘 하든 신경쓰지않고, 단지 push할 뿐입니다.

이벤트의 연속이라는 개념만으로도 훌륭하지만, **RxJS를 "이벤트계의 lodash"로 만들어준 것은 연산자(Operators)때문입니다**

## 연산자(operators)

연산자는 원본데이터를 조작하여 옵저버블로 변환된 값을 제공합니다. 만약 당신이 자바스크립트의 `객체` 메소드에 익숙하다면, RxJS의 수많은 연산자들도 눈에 익을 것입니다. 예를 들어, 만약 방출된 값을 바꾸길 원한다면, [`map`](../operators/transformation/map.md) 메소드를 사용하면 됩니다:

```javascript
import { of } from 'rxjs';
import { map } from 'rxjs/operators';
/*
 *  'of' 를 통해 값을 순차적으로 전달할 수 있습니다
 *  다음과 같은 경우라면, 1,2,3,4,5 를 순서대로 뱉어낼 것입니다.
 */
const dataSource = of(1, 2, 3, 4, 5);

// 원본 옵저버블을 구독하기
const subscription = dataSource
  .pipe(
    // 방출된 값에 각각 1씩 더하기
    map(value => value + 1)
  )
  // log: 2, 3, 4, 5, 6
  .subscribe(value => console.log(value));
```

또 만약 특정한 값을 거르고 싶다면, [`filter`](../operators/filtering/filter.md) 를 사용하면 됩니다:

```javascript
import { of } from 'rxjs';
import { filter } from 'rxjs/operators';

const dataSource = of(1, 2, 3, 4, 5);

// 원본 옵저버블을 구독하기
const subscription = dataSource
  .pipe(
    // 2보다 크거나 같은 값만 받는다
    filter(value => value >= 2)
  )
  // log: 2, 3, 4, 5
  .subscribe(value => console.log(value));
```

대부분의 경우, **그 문제를 해결해줄 수 있는 연산자**가 이미 존재하고 있을 확률이 큽니다. RxJS의 세계에 처음 발을 담궜다면, 수많은 연산자의 갯수에 압도당할 수 있습니다. 하지만 정말 자주 쓰이는 몇가지의 연산자를 사용해보는 것으로 시작해보세요. 시간이 지나면서, 처리하기 곤란한 상황에 마주했을 때, 여러분은 연산자의 유연성에 감탄할 것입니다.

**이미 위 예시에서 눈치챘을 수도 있겠지만, 연산자들은 파이프 내부에 존재합니다**

## 파이프

`파이프`함수는 연산자 조립 라인이라고 보면 됩니다. 공장의 원자재가 완제품이 되기까진 일련의 단계를 거쳐야하는 것처럼, 원본 데이터는 사용자의 입맛에 맞게 데이터를 조작, 필터링, 그리고 변환시킬 수 있는 `파이프` 라고 불리는 과정을 거치게됩니다. `pipe` 함수 안에서는 옵저버블 체인을 이용하여 5개, 혹은 그 이상의 연산자를 사용하는 일도 가능합니다.

옵저버블을 활용한 자동완성 기능을 예로 들면, HTTP 리퀘스트와 디스플레이 과정을 모두 부드럽게 처리하기위해 여러가지의 연산자를 사용할 것입니다:

```javascript
// 파이프 체인 연산자를 사용한 텍스트박스의 옵저버블 예시
inputValue
  .pipe(
    // 200ms 정지.
    debounceTime(200),
    // 값이 똑같으면, 무시.
    distinctUntilChanged(),
    // 아직 요청중일 때 업데이트된 값이 수신되는 경우, 이전 요청을 취소하고 새로운 옵저버블로 '변경'.
    switchMap(searchTerm => typeaheadApi.search(searchTerm))
  )
  // subscription 생성.
  .subscribe(results => {
    // dom 업데이트.
  });
```

**내게 필요한 연산자가 무엇인지 어떻게 알 수 있을까요? 좋은 소식은 바로...**

## 연산자를 공통 카테고리로 묶어 분류할 수 있다는 점입니다.

내게 필요한 연산자를 찾을 때 첫번째로 생각해야할 것은 관련 카테고리를 찾는 것입니다. 원본 데이터를 필터링해야합니까? [`필터링`](../operators/filtering/) 연산자를 찾아보세요. 버그를 추적하거나, 옵저버블의 흐름을 통해 데이터 플로우를 디버깅해야합니까? [`유틸리티`](../operators/utility/) 연산자가 도와줄 것입니다. **연산자 카테고리는 다음과 같습니다.**

### [생성 연산자](../operators/creation/)

이 연산자들은 대부분의 것들을 옵저버블로 만들어줍니다. 일반적인 케이스부터 정말 특별한 케이스에 이르기까지, 모든 것들을 하나의 데이터흐름으로 바꿀 수 있습니다.

예를 들어, 사용자가 문서를 스크롤할 때 진행 표시줄을 만든다고 해봅시다. [`fromEvent`](../operators/creation/fromevent.md) 연산자를 통해 스크롤 이벤트를 데이터 흐름으로 바꿀 수 있습니다:

```javascript
fromEvent(scrollContainerElement, 'scroll')
  .pipe(
    // 연산자들의 사용법은 나중에 자세히하고, 여기선 넘어가보죠.
    takeUntil(userLeavesArticle)
  )
  .subscribe(event => {
    // 계산 후 DOM업데이트
  });
```

가장 많이 사용되는 생성 연산자에는 [`of`](../operators/creation/of.md), [`from`](../operators/creation/from.md), 그리고[`fromEvent`](../operators/creation/fromevent.md) 등이 있습니다.

### [조합 연산자](../operators/combination/)

The combination operators allow the joining of information from multiple observables. Order, time, and structure of emitted values is the primary variation among these operators.

For example, we can combine updates from multiple data sources to perform a calculation:

```javascript
// give me the last emitted value from each source, whenever either source emits
combineLatest(sourceOne, sourceTwo).subscribe(
  ([latestValueFromSourceOne, latestValueFromSourceTwo]) => {
    // perform calculation
  }
);
```

The most commonly used combination operators are [`combineLatest`](../operators/combination/combinelatest.md), [`concat`](../operators/combination/concat.md), [`merge`](../operators/combination/merge.md), [`startWith`](../operators/combination/startwith.md), and [`withLatestFrom`](../operators/combination/withlatestfrom.md).

### [Error handling operators](../operators/error_handling/)

The error handling operators provide effective ways to gracefully handle errors and perform retries, should they occur.

For example, we can use [`catchError`](https://github.com/JUNWOO45/learn-rxjs-korean/tree/8c9661a5ef018c109eae0814410977d79cebac1b/operators/error_handling/catcherror.md) to safeguard against failed network requests:

```javascript
source
  .pipe(
    mergeMap(value => {
      return makeRequest(value).pipe(
        catchError(handleErrorByReturningObservable)
      );
    })
  )
  .subscribe(value => {
    // take action
  });
```

The most commonly used error handling operators is [`catchError`](https://github.com/JUNWOO45/learn-rxjs-korean/tree/8c9661a5ef018c109eae0814410977d79cebac1b/operators/error_handling/catcherror.md).

### [Filtering operators](../operators/filtering/)

The filtering operators provide techniques for accepting - or declining - values from an observable source and dealing with backpressure, or the build up of values within a stream.

For example, we can use the [`take`](../operators/filtering/take.md) operator to capture only the first `5` emitted values from a source:

```javascript
source.pipe(take(5)).subscribe(value => {
  // take action
});
```

The most commonly used filtering operators are [`debounceTime`](../operators/filtering/debouncetime.md), [`distinctUntilChanged`](../operators/filtering/distinctuntilchanged.md), [`filter`](../operators/filtering/filter.md), [`take`](../operators/filtering/take.md), and [`takeUntil`](../operators/filtering/takeuntil.md).

### [Multicasting operators](../operators/multicasting/)

In RxJS observables are cold, or unicast \(one source per subscriber\) by default. These operators can make an observable hot, or multicast, allowing side-effects to be shared among multiple subscribers.

For example, we may want late subscribers to share, and receive the last emitted value from an active source:

```javascript
const source = data.pipe(shareReplay());

const firstSubscriber = source.subscribe(value => {
  // perform some action
});

// sometime later...

// second subscriber gets last emitted value on subscription, shares execution context with 'firstSubscriber'
const secondSubscriber = source.subscribe(value => {
  // perform some action
});
```

The most commonly used multicasting operator is [`shareReplay`](../operators/multicasting/sharereplay.md).

### [Transformation operators](../operators/transformation/)

Transforming values as they pass through an operator chain is a common task. These operators provide transformation techniques for nearly any use-case you will encounter.

For example, we may want to accumulate a state object from a source over time, similar to [Redux](https://redux.js.org/):

```javascript
source
  .pipe(
    scan((accumulatedState, currentState) => {
      return { ...accumulatedState, ...currentState };
    })
  )
  .subscribe();
```

The most commonly used transformation operators are [`concatMap`](../operators/transformation/concatmap.md), [`map`](../operators/transformation/map.md), [`mergeMap`](../operators/transformation/mergemap.md), [`scan`](../operators/transformation/scan.md), and [`switchMap`](../operators/transformation/switchmap.md).

## Operators have common behaviors

While operators can be grouped into common categories, operators within a category often share common behavior. By recognizing this common behavior you can start creating a [_'choose your own operator'_ tree](https://rxjs-dev.firebaseapp.com/operator-decision-tree) in your mind.

**For instance, a large amount of operators can be grouped into...**

#### Operators that flatten

Or, in other words, operators that manage the subscription of an inner observable, emitting those values into a single observable source. One common use case for flattening operators is handling HTTP requests in a observable or promise based API, but that is really just scratching the surface:

```javascript
fromEvent(button, 'click')
  .pipe(
    mergeMap(value => {
      // this 'inner' subscription is managed by mergeMap, with response value emitted to observer
      return makeHttpRequest(value);
    })
  )
  .subscribe(response => {
    // do something
  });
```

**We can then divide the flattening operators into common behaviors like...**

#### Operators that `switch`

Like a light switch, `switch` based operators will turn off \(unsubscribe\) the current observable and turn on a new observable on emissions from the source. Switch operators are useful in situations you don't want \(or need\) more than one active observable at a time:

```javascript
inputValueChanges
  // only the last value is important, if new value comes through cancel previous request / observable
  .pipe(
    // make GET request for data
    switchMap(requestObservable)
  )
  .subscribe();
```

Switch based operators include `switchAll`, [`switchMap`](../operators/transformation/switchmap.md), and [`switchMapTo`](../operators/transformation/switchmapto.md).

#### Operators that `concat`

Comparable to a line at the ATM machine, the next transaction can't begin until the previous completes. In observable terms, only one subscription will occur at a time, in order, triggered by the completion of the previous. These are useful in situations where order of execution is important:

```javascript
concat(
  firstObservable,
  // will begin when 'firstObservable` completes
  secondObservable,
  // will begin when 'secondObservable` completes
  thirdObservable
).subscribe(values => {
  // take action
});
```

Concat based operators include [`concat`](../operators/combination/concat.md), [`concatAll`](../operators/combination/concatall.md), [`concatMap`](../operators/transformation/concatmap.md), and [`concatMapTo`](../operators/transformation/concatmapto.md).

#### Operators that `merge`

Like your merging lane on the interstate, merge based operators support multiple active observables flowing into one lane in a first come first serve basis. Merge operators are useful in situations where you want to trigger an action when an event from one of many sources occurs:

```javascript
merge(firstObservable, secondObservable)
  // any emissions from first or second observable as they occur
  .pipe(mergeMap(saveActivity))
  .subscribe();
```

Merge based operators include [`merge`](../operators/combination/merge.md), [`mergeMap`](../operators/transformation/mergemap.md), `mergeMapTo` and [`mergeAll`](../operators/combination/mergeall.md).

## Other similarities between operators

There are also operators that share a similar goal but offer flexibility in their triggers. For instance, for unsubscribing from an observable after a specific condition is met, we could use:

1. [`take`](../operators/filtering/take.md) when we know we only ever want `n`

   values.

2. [`takeLast`](../operators/filtering/takelast.md) when you just want the last

   `n` values.

3. [`takeWhile`](../operators/filtering/takewhile.md) when we have a predicate

   expression to supply.

4. [`takeUntil`](../operators/filtering/takeuntil.md) when we only want the

   source to remain active until another source emits.

While the number of RxJS operators can seem overhelming at first, these common behaviors and patterns can bridge the gap rather quickly while learning RxJS.

## What does this get me?

As you become more familiar with push based programming through Observables, you can begin to model all async behavior in your applications through observable streams. This opens up simple solutions and flexibility for notably complex behavior.

For instance, suppose we wanted to make a request which saved user activity when they answered a quiz question. Our initial implementation may use the [`mergeMap`](https://github.com/JUNWOO45/learn-rxjs-korean/tree/8c9661a5ef018c109eae0814410977d79cebac1b/opearators/transformation/mergemap.md) operator, which fires off a save request on each event:

```javascript
const formEvents = fromEvent(formField, 'click');
const subscription = formEvents
  .pipe(
    map(convertToAppropriateValue),
    mergeMap(saveRequest)
  )
  .subscribe();
```

Later, it's determined that we need to ensure order of these saves. Armed with the knowledge of operator behavior from above, instead of implementing a complex queueing system we can instead replace the [`mergeMap`](../operators/transformation/mergemap.md) operator with [`concatMap`](../operators/transformation/concatmap.md) and push up our changes:

```javascript
const formEvents = fromEvent(formField, 'click');
const subscription = formEvents
  .pipe(
    map(convertToAppropriateValue),
    // now the next request won't begin until the previous completes
    concatMap(saveRequest)
  )
  .subscribe();
```

With the change of one word we are now queueing our event requests, and this is just scratching the surface of what is possible!

## Keep Going!

Learning RxJS can be intimidating, but it's a path I promise is worth the investment. If some of these concepts are still fuzzy \(or make no sense at all!\), don't worry! It will all click soon.

Start checking out the operators on the left hand side of the site for common examples and use-cases, as well as the additional [introductory resources](../../#introductory-resources) we have collected from across the web. Good luck and enjoy your journey to becoming a reactive programming expert!


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
2. 매 클릭 이벤트 마다 subscribe 메소드와 함께 보낸 함수 \(observer\) 를 실행합니다.

3. Return a subscription object with an `unsubscribe` which contains clean up

   logic, like removing appropriate event listeners.

The subscribe method also accepts an object map to handle the case of error or completion. You probably won't use this as much as simply supplying a function, but it's good to be aware of should the need arise:

```javascript
// instead of a function, we will pass an object with next, error, and complete methods
const subscription = myObservable.subscribe({
  // on successful emissions
  next: event => console.log(event),
  // on errors
  error: error => console.log(error),
  // called once on completion
  complete: () => console.log('complete!')
});
```

It's important to note that each subscription will create a new execution context. This means calling `subscribe` a second time will create a new event listener:

```javascript
// addEventListener called
const subscription = myObservable.subscribe(event => console.log(event));

// addEventListener called again!
const secondSubscription = myObservable.subscribe(event => console.log(event));

// clean up with unsubscribe
subscription.unsubscribe();
secondSubscription.unsubscribe();
```

By default, a subscription creates a one on one, one-sided conversation between the observable and observer. This is like your boss \(the observable\) yelling \(emitting\) at you \(the observer\) for merging a bad PR. This is also known as **unicasting**. If you prefer a conference talk scenario - one observable, many observers - you will take a different approach which includes **multicasting** with `Subjects` \(either explicitly or behind the scenes\). More on that in a future article!

It's worth noting that when we discuss an Observable source emitting data to observers, this is a push based model. The source doesn't know or care what subscribers do with the data, it simply pushes it down the line.

While working on a stream of events is nice, it's only so useful on its own. **What makes RxJS the "lodash for events" are its...**

## Operators

Operators offer a way to manipulate values from a source, returning an observable of the transformed values. Many of the RxJS operators will look familiar if you are used to JavaScripts `Array` methods. For instance, if you want to transform emitted values from an observable source, you can use [`map`](../operators/transformation/map.md):

```javascript
import { of } from 'rxjs';
import { map } from 'rxjs/operators';
/*
 *  'of' allows you to deliver values in a sequence
 *  In this case, it will emit 1,2,3,4,5 in order.
 */
const dataSource = of(1, 2, 3, 4, 5);

// subscribe to our source observable
const subscription = dataSource
  .pipe(
    // add 1 to each emitted value
    map(value => value + 1)
  )
  // log: 2, 3, 4, 5, 6
  .subscribe(value => console.log(value));
```

Or if you want to filter for specific values, you can use [`filter`](../operators/filtering/filter.md):

```javascript
import { of } from 'rxjs';
import { filter } from 'rxjs/operators';

const dataSource = of(1, 2, 3, 4, 5);

// subscribe to our source observable
const subscription = dataSource
  .pipe(
    // only accept values 2 or greater
    filter(value => value >= 2)
  )
  // log: 2, 3, 4, 5
  .subscribe(value => console.log(value));
```

In practice, if there is a problem you need to solve, it's more than likely **there is an operator for that**. And while the sheer number of operators can be overwhelming as you begin your RxJS journey, you can narrow it down to a small handful \(and we will\) to start being effective. Over time, you will come to appreciate the flexibility of the operator library when obscure scenarios inevitably arrive.

**One thing you may have noticed in the example above, is operators exist within a...**

## Pipe

The `pipe` function is the assembly line from your observable data source through your operators. Just like raw material in a factory goes through a series of stops before it becomes a finished product, source data can pass through a `pipe`-line of operators where you can manipulate, filter, and transform the data to fit your use case. It's not uncommon to use 5 \(or more\) operators within an observable chain, contained within the `pipe` function.

For instance, a typeahead solution built with observables may use a group of operators to optimize both the request and display process:

```javascript
// observable of values from a text box, pipe chains operators together
inputValue
  .pipe(
    // wait for a 200ms pause
    debounceTime(200),
    // if the value is the same, ignore
    distinctUntilChanged(),
    // if an updated value comes through while request is still active cancel previous request and 'switch' to new observable
    switchMap(searchTerm => typeaheadApi.search(searchTerm))
  )
  // create a subscription
  .subscribe(results => {
    // update the dom
  });
```

**But how do you know which operator fits your use-case? The good news is...**

## Operators can be grouped into common categories

The first stop when looking for the correct operator is finding a related category. Need to filter data from a source? Check out the [`filtering`](../operators/filtering/) operators. Trying to track down a bug, or debug the flow of data through your observable stream? There are [`utility`](../operators/utility/) operators that will do the trick. **The operator categories include...**

### [Creation operators](../operators/creation/)

These operators allow the creation of an observable from nearly anything. From generic to specific use-cases you are free to turn everything into a stream.

For example, suppose we are creating a progress bar as a user scrolls through an article. We could turn the scroll event into a stream by utilizing the [`fromEvent`](../operators/creation/fromevent.md) operator:

```javascript
fromEvent(scrollContainerElement, 'scroll')
  .pipe(
    // we will discuss cleanup strategies like this in future article
    takeUntil(userLeavesArticle)
  )
  .subscribe(event => {
    // calculate and update DOM
  });
```

The most commonly used creation operators are [`of`](../operators/creation/of.md), [`from`](../operators/creation/from.md), and [`fromEvent`](../operators/creation/fromevent.md).

### [Combination operators](../operators/combination/)

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


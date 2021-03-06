# RxJS 입문서

RxJS를 처음 접하시나요? 이 페이지에서는 RxJS를 이해하는데 필요한 모든 주요 개념들을 배우고, RxJS를 다뤄볼 것입니다. 준비되었으면 시작해봅시다!

## 옵저버블이란?

옵저버블은 시간의 흐름에 따라 도착하는 스트림, 또는 데이터의 출처를 의미합니다. 우린 거의 대부분의 것들에서 옵저버블을 만들어낼 수 있지만, 이벤트에서 사용되어지는 일이 가장 흔합니다. 이벤트는 마우스의 움직임, 버튼 클릭,텍스트 필드를 채워넣는 행위, 라우트 변경 등을 의미합니다. 옵저버블을 생성하는 가장 쉬운 방법은 내장된 생성 함수를 사용하는 것입니다. 예를 들어, 마우스 클릭 이벤트의 옵저버블을 만들기 위해 [`fromEvent`](../recipes-1/creation/fromevent.md) 함수를 사용할 수 있습니다:

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

Subscriptions은 모든 것을 동작하게 합니다. 이걸 수도꼭지에 비유할 수 있는데, 누군가가 손잡이를 돌리기만 하면 물줄기\(옵저버블\)가 흐르거나 멈출 수 있습니다. `subscriber` 가 이러한 역할을 합니다.

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

위 예시에서,myObservable.subscribe\(\)\` 은 다음과 같은 일을 합니다:

1. 버튼에 클릭 이벤트에 대한 이벤트 리스너를 설정합니다.
2. 매 클릭 이벤트 마다 subscribe 메소드와 함께 넘겨준 함수 \(observer\) 를 실행합니다.
3. 적절한 이벤트 리스너 삭제와 같은 일을 하는 `unsubscribe` 와 함께 Subscription 객체를 반환합니다.

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

기본적으로, Subscription은 옵저버블과 옵저버사이의 1대1이면서도 일방적인 데이터흐름을 만들어냅니다. 마치 여러분의 상사\(옵저버블\)가 구린 PR을 머지했다고 당신\(옵저버\)에게 소리치는 것\(방출\)과 비슷합니다. 바로 **unicasting** 으로 알려져있는 방법이죠. 만약 당신이 컨퍼런스 대화를 좋아한다면 - 한 명의 옵저버블과 수많은 옵저버들 - 당신은 **multicasting** 을 포함하는 다른 방법을 취해야 할 것입니다. 이와 관련해서는 나중에 더 알아보죠!

옵저버에게 데이터를 방출하는 옵저버블은, push 기반의 모델이라는 점을 유의해야합니다. Subscriber가 이 데이터로 뭘 하든 신경쓰지않고, 단지 push할 뿐입니다.

이벤트의 연속이라는 개념만으로도 훌륭하지만, **RxJS를 "이벤트계의 lodash"로 만들어준 것은 연산자\(Operators\)때문입니다**

## 연산자\(operators\)

연산자는 원본데이터를 조작하여 옵저버블로 변환된 값을 제공합니다. 만약 당신이 자바스크립트의 `객체` 메소드에 익숙하다면, RxJS의 수많은 연산자들도 눈에 익을 것입니다. 예를 들어, 만약 방출된 값을 바꾸길 원한다면, [`map`](../recipes-1/transformation/map.md) 메소드를 사용하면 됩니다:

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

또 만약 특정한 값을 거르고 싶다면, [`filter`](../recipes-1/filtering/filter.md) 를 사용하면 됩니다:

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

내게 필요한 연산자를 찾을 때 첫번째로 생각해야할 것은 관련 카테고리를 찾는 것입니다. 원본 데이터를 필터링해야합니까? [`필터링`](../recipes-1/filtering/) 연산자를 찾아보세요. 버그를 추적하거나, 옵저버블의 흐름을 통해 데이터 플로우를 디버깅해야합니까? [`유틸리티`](../recipes-1/utility/) 연산자가 도와줄 것입니다. **연산자 카테고리는 다음과 같습니다.**

### [생성 연산자](../recipes-1/creation/)

이 연산자들은 대부분의 것들을 옵저버블로 만들어줍니다. 일반적인 케이스부터 정말 특별한 케이스에 이르기까지, 모든 것들을 하나의 데이터흐름으로 바꿀 수 있습니다.

예를 들어, 사용자가 문서를 스크롤할 때 진행 표시줄을 만든다고 해봅시다. [`fromEvent`](../recipes-1/creation/fromevent.md) 연산자를 통해 스크롤 이벤트를 데이터 흐름으로 바꿀 수 있습니다:

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

가장 많이 사용되는 생성 연산자에는 [`of`](../recipes-1/creation/of.md), [`from`](../recipes-1/creation/from.md), 그리고[`fromEvent`](../recipes-1/creation/fromevent.md) 등이 있습니다.

### [조합 연산자](../recipes-1/combination/)

조합 연산자는 여러 옵저버블의 값을 결합해줍니다. 조합 연산자는 주로 방출된 값의 순서, 시간 및 구조를 변형합니다.

예를 들어, 여러 데이터 값을 결합하여 계산을 할 수 있습니다:

```javascript
// 원본데이터가 방출될 때마다, 각 원본데이터로부터 마지막으로 방출된 값을 사용하여
combineLatest(sourceOne, sourceTwo).subscribe(
  ([latestValueFromSourceOne, latestValueFromSourceTwo]) => {
    // 계산을 수행.
  }
);
```

조합 연산자 중에서는 [`combineLatest`](../recipes-1/combination/combinelatest.md), [`concat`](../recipes-1/combination/concat.md), [`merge`](../recipes-1/combination/merge.md), [`startWith`](../recipes-1/combination/startwith.md), 그리고[`withLatestFrom`](../recipes-1/combination/withlatestfrom.md) 가 자주 사용됩니다.

### [에러 핸들링 연산자](../recipes-1/error_handling/)

에러 핸들링 연산자는 오류가 발생할 경우 우아하게 오류를 처리하고 효과적으로 재시도를 수행하는 방법을 제공합니다.

예를 들어, [`catchError`](https://github.com/JUNWOO45/learn-rxjs-korean/tree/8c9661a5ef018c109eae0814410977d79cebac1b/operators/error_handling/catcherror.md) 를 사용하여 네트워크 요청이 실패했을 경우를 대비할 수 있습니다:

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
    // 네트워크 요청이 실패했을 경우의 로직입력
  });
```

에러 핸들링 연산자에서는 [`catchError`](https://github.com/JUNWOO45/learn-rxjs-korean/tree/8c9661a5ef018c109eae0814410977d79cebac1b/operators/error_handling/catcherror.md) 가 가장 많이 쓰입니다.

### [필터링 연산자](../recipes-1/filtering/)

필터링 연산자는 옵저버블 원본 데이터의 값을 받거나 감소시키는 방법을 제공하고, backpressure를 다루거나, 스트림 내에서의 값 증가를 처리할 수 있게 도와줍니다.

예를 들어, [`take`](../recipes-1/filtering/take.md) 연산자를 사용해서 원본데이터로부터 가장 처음 방출되는 `5` 값을 잡아낼 수 있습니다:

```javascript
source.pipe(take(5)).subscribe(value => {
  // 로직 수행
});
```

가장 자주 사용되는 필터링 연산자에는 [`debounceTime`](../recipes-1/filtering/debouncetime.md), [`distinctUntilChanged`](../recipes-1/filtering/distinctuntilchanged.md), [`filter`](../recipes-1/filtering/filter.md), [`take`](../recipes-1/filtering/take.md), 그리고[`takeUntil`](../recipes-1/filtering/takeuntil.md) 등이 있습니다.

### [멀티캐스팅 연산자](../recipes-1/multicasting/)

기본적으로 RxJS의 옵저버블은, cold하고 unicast\(하나의 소스에 하나의 subscriber\)한 성격을 가지고 있습니다. 이 연산자들은 옵저버블을 hot하고 멀티캐스트가 가능하게 바꿔주어서, 여러 subscribers들이 사이드이펙트를 공유할 수 있도록 만들어줍니다.

예를 들어, 늦게 실행되는 subscribers가 마지막으로 방출된 값을 공유하고, 또한 값을 받기를 원할 수 있습니다.

```javascript
const source = data.pipe(shareReplay());

const firstSubscriber = source.subscribe(value => {
  // 무언가를 하고,
});

// 시간이 지난 뒤..

// 두번째 subscriber는 구독 시 마지막으로 방출된 값을 받고, 'firstSubscriber'와 실행컨텍스트를 공유한다.
const secondSubscriber = source.subscribe(value => {
  // 무언가를 하고.
});
```

멀티캐스팅 연산자 중에서는 [`shareReplay`](../recipes-1/multicasting/sharereplay.md) 가 가장 많이 쓰입니다.

### [변환 연산자](../recipes-1/transformation/)

연산자 체인을 통과하며 값을 변화시키는 것은 매우 일반적인 일입니다. 변환 연산자들을 여러분이 마주칠 거의 모든 상황에서 사용가능한 값을 변화시키는 다양한 방법들을 제공해줍니다.

예를 들어, [Redux](https://redux.js.org/) 와 비슷하게, 시간이 지남에 따라 원본 데이터로부터 상태값을 축적시키길 원할 수 있습니다:

```javascript
source
  .pipe(
    scan((accumulatedState, currentState) => {
      return { ...accumulatedState, ...currentState };
    })
  )
  .subscribe();
```

변환 연산자에서는 [`concatMap`](../recipes-1/transformation/concatmap.md), [`map`](../recipes-1/transformation/map.md), [`mergeMap`](../recipes-1/transformation/mergemap.md), [`scan`](../recipes-1/transformation/scan.md), 그리고[`switchMap`](../recipes-1/transformation/switchmap.md) 가 가장 많이 사용됩니다.

## 연산자들은 공통적인 행동을 수행합니다.

같은 카테고리에 속하는 연산자들은 종종 비슷한 동작을 공유합니다. 이러한 공통 행위를 인식하면, 마음 속에서 [_'당신만의 연산자 선택 트리'_ ](https://rxjs-dev.firebaseapp.com/operator-decision-tree) 를 만들 수 있습니다.

**예를 들어, 수많은 연산자들을 다음과 같이 분류할 수 있습니다...**

#### 평탄화\(flatten\) 연산자

또는 다른 말로, 값들을 하나의 옵저버블 소스로 방출하면서 내부 옵저버블의 구독을 관리하는 연산자. 평탄화\(flatten\) 연산자의 대표적인 예는, HTTP 요청을 프로미스나 옵저버블 기반으로 처리하는 것이지만, 이것은 정말 겉핥기에 불과합니다.

```javascript
fromEvent(button, 'click')
  .pipe(
    mergeMap(value => {
      // 이러한 '내부' subscription은 응답값을 옵저버에게로 방출하며 mergeMap을 통해 관리합니다
      return makeHttpRequest(value);
    })
  )
  .subscribe(response => {
    // 로직 수행
  });
```

**또한, 평탄화 연산자를 다음과같은 분류로 나눌 수 있습니다**

#### `switch` 연산자

마치 전등처럼, `switch` 를 기반으로한 연산자는 현재 옵저버블을 끄고\(unsubscribe\) 데이터로부터 방출되는 새로운 옵저버블을 반환할 것입니다. Switch 연산자는 한 번에 두 개 이상의 옵저버블을 원하지 않는 경우에 유용합니다:

```javascript
inputValueChanges
  // 마지막 값이 중요하기때문에, 만약 새로운 값이 넘어온다면, 이전 리퀘스트나 옵저버블은 취소됩니다.
  .pipe(
    // GET 리퀘스트를 보내봅시다.
    switchMap(requestObservable)
  )
  .subscribe();
```

Switch 기반의 연산자에는 `switchAll`, [`switchMap`](../recipes-1/transformation/switchmap.md), 그리고 [`switchMapTo`](../recipes-1/transformation/switchmapto.md) 가 있습니다.

#### `concat` 연산자

이전 작업이 완료되기 전까지는 다음 작업도 시작될 수 없는, ATM 기계 뒤에 줄서있는 모습으로 비유할 수 있습니다. 옵저버블의 관점에서 본다면, 한 번에 하나의 subscription만 가능하고, 순서를 지켜야하고, 또한 이전 작업이 완료되어야 다음 작업을 진행할 수 있습니다. 이 연산자는 실행 순서가 중요한 상황에서 매우 유용하게 쓰입니다:

```javascript
concat(
  firstObservable,
  // 'firstObservable`이 완료되어야 실행될 것입니다
  secondObservable,
  // 'secondObservable`이 완료되어야 실행될 것입니다
  thirdObservable
).subscribe(values => {
  // 로직 수행
});
```

Concat 연산자에는 [`concat`](../recipes-1/combination/concat.md), [`concatAll`](../recipes-1/combination/concatall.md), [`concatMap`](../recipes-1/transformation/concatmap.md), 그리고[`concatMapTo`](../recipes-1/transformation/concatmapto.md) 가 있습니다.

#### `merge` 연산자

고속도로에서 여러개였던 차선이 하나의 차선으로 합쳐지는 모습처럼, merge 기반의 연산자는 선착순으로 하나의 차선으로 흐르는 복수개의 활성 옵저버블을 지원합니다. Merge 연산자는 여러 소스 중 하나에서 이벤트를 발생시키고, 그 이벤트가 어떠한 액션을 불러일으킬 때 유용합니다:

```javascript
merge(firstObservable, secondObservable)
  // 첫번째, 혹은 두번째 옵저버블에서 발생하는 모든 결과물
  .pipe(mergeMap(saveActivity))
  .subscribe();
```

Merge 기반의 연산자에는 [`merge`](../recipes-1/combination/merge.md), [`mergeMap`](../recipes-1/transformation/mergemap.md), `mergeMapTo` 그리고 [`mergeAll`](../recipes-1/combination/mergeall.md) 이 있습니다.

## 연산자들 사이의 또다른 공통점

비슷한 동작을 하면서도, 유연성을 더해주는 연산자도 있다. 예를 들어, 특정 조건이 충족된 후, 옵저버블을 구독 취소\(unsubscribe\)하려는 경우에는:

1. [`take`](../recipes-1/filtering/take.md) 정확히 `n` 이라는 값만을 원할 때

   values.

2. [`takeLast`](../recipes-1/filtering/takelast.md) 가장 마지막 `n` 값을 원할 때
3. [`takeWhile`](../recipes-1/filtering/takewhile.md) 표현식이 충족되었을 때
4. [`takeUntil`](../recipes-1/filtering/takeuntil.md) 다른 소스가 값을 방출\(emit\)될 때까지 소스가 active하게 유지되기를 원할 때

처음 RxJS를 보면 연산자들이 지나치게 많은 것처럼 보일 수 있지만, 이러한 일반적인 행동과 패턴을 알고 RxJS를 배우면서 더욱 쉽게 접근할 수 있습니다.

## 이게 나한테 무슨 의미가 있지?

옵저버블을 통한 push기반의 프로그래밍에 익숙해지면, 옵저버블 스트림을 통해 여러분의 애플리케이션의 모든 비동기 동작을 모델링해나갈 수 있게됩니다. 이러한 방식은 매우 복잡한 행동을 위한 간단한 해결책과 유연성을 제공해줍니다.

예를 들어, 만약 사용자가 퀴즈 질문에 답했을 때 사용자의 활동을 저장하는 요청을 하고 싶다고 가정해봅시다. 초기 구현 시에는 [`mergeMap`](https://github.com/JUNWOO45/learn-rxjs-korean/tree/8c9661a5ef018c109eae0814410977d79cebac1b/opearators/transformation/mergemap.md) 연산자를 사용하여 각각의 이벤트에대한 저장 요청을 실행할 것입니다:

```javascript
const formEvents = fromEvent(formField, 'click');
const subscription = formEvents
  .pipe(
    map(convertToAppropriateValue),
    mergeMap(saveRequest)
  )
  .subscribe();
```

시간이 지나, 순서 또한 저장할 필요가 있다고 깨닫게 되었다고 해봅시다. 위에서 배운 지식으로 무장한다면, 복잡한 대기열 시스템을 구현하는 대신, 단순히 [`mergeMap`](../recipes-1/transformation/mergemap.md) 연산자를 [`concatMap`](../recipes-1/transformation/concatmap.md) 으로 교체하는 것만으로 우리의 목적을 달성할 수 있습니다.

```javascript
const formEvents = fromEvent(formField, 'click');
const subscription = formEvents
  .pipe(
    map(convertToAppropriateValue),
    // 이제 다음 리퀘스트는 이전 작업이 완료되기 전까지는 절대 시작하지 않을 것입니다
    concatMap(saveRequest)
  )
  .subscribe();
```

단어 하나의 변경으로 우리는 이벤트 리퀘스트 요청을 줄세워서 대기할 수 있게 되었고, 이러한 예시는 빙산의 일각에 불과합니다!

## 계속 나아가세요!

RxJS를 배우는 것은 어렵지만, 투자할 만한 가치가 있다고 확신합니다. 개념들 중 일부가 여전히 모호해도 \(전혀 이해가 가지 않아도!\) 걱정마세요! 금방 이해가 갈 거에요.

사이트 왼쪽에 있는 일반적인 예와 사용 사례들이 적혀있는 연산자 항목과, 웹을 통해 수집한 후 추가한 [입문자들을 위한 자료](../../#introductory-resources) 를 살펴보세요. 그리고 리액티브 프로그래밍 전문가가 되기위한 여정을 즐기세요. 행운을 빕니다!


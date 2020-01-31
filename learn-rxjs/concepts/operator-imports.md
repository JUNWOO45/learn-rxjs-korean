# 연산자 imports의 이해

여러분들은 또한 RxJS 연산자를 가져올 때 에러를 겪었을 수 있습니다. 프로젝트에 연산자를 가져오는 방법 중 가장 흔한 방법은 아래처럼 import하는 것입니다:

```javascript
import 'rxjs/add/operator/take';
```

이렇게하면 프로젝트 전반에 걸쳐 사용할 수 있는 옵저버블 프로토타입에 가져온 연산자가 추가됩니다:

[\(Source\)](https://github.com/ReactiveX/rxjs/blob/master/src/add/operator/take.ts)

```javascript
import { Observable } from '../../Observable';
import { take } from '../../operator/take';

Observable.prototype.take = take;

declare module '../../Observable' {
  interface Observable<T> {
    take: typeof take;
  }
}
```

이러한 방법은 개인 프로젝트나 개인 모듈에서는 문제가 없지만, 이렇게 가져온 것들을 조직 전체에서 사용할 [npm](https://www.npmjs.com/) 패키지나 라이브러리로 사용할 때 문제가 발생합니다. 

## 간단한 예시

문제가 어떻게 발생하는지 알아보기위해, **A라는 사람**이 공용 앵귤러 컴포넌트 라이브러리를 만들었다고 가정해봅시다. 이 라이브러리에서 몇가지 연산자가 필요해서 다음과같이 연산자들을 추가했습니다:

_some-public-library.ts_

```javascript
import 'rxjs/add/operator/take';
import 'rxjs/add/operator/concatMap';
import 'rxjs/add/operator/switchMap';
```

**B라는 사람**도 라이브러리를 설치했습니다. B는 개인적으로 그 연산자들을 가져온 적이 없지만, 연산자에 접근해서 사용할 수 있는 상태입니다. _별 문제가 아닐 수 있지만, 혼란스러울 수 있습니다._ 당신은 그 라이브러리와 연산자들을 계속 사용할 것이고..

한 달이 지난 어느날, **A 라는 사람**은 라이브러리를 업데이트시키려고 합니다. A는 더이상 `switchMap` 과 `concatMap` 를 쓸 필요가 없어, import문을 삭제해버립니다:

_some-public-library.ts_

```javascript
import 'rxjs/add/operator/take';
```

**B라는 사람**도 의존성을 업그레이드한 뒤, 빌드를 시도하지만, 실패합니다. B는 스스로 `switchMap` 이나 `concatMap` 가져온 적이 없이, 다른 사람이 가져온 연산자를 **그냥 쓰고 있었을 뿐입니다.** B가 이러한 상황이 문제가 될 수 있다는 것을 미리 알지 못했다면, 에러를 추적하는데 시간이 걸릴 지 모릅니다.

## 해결 방법

연산자를 아래와 같이 가져오지 말고,

```javascript
import 'rxjs/add/operator/take';
```

이렇게 가져와보세요:

```javascript
import { take } from 'rxjs/operator/take';
```

이러한 방법은 연산자를 `옵저버블` 프로토타입이 아닌, 연산자를 직접적으로 호출할 수 있게 해줍니다:

```javascript
import { take } from 'rxjs/operator/take';
import { of } from 'rxjs/observable/of';

take.call(
  of(1,2,3), 
  2
);
```

하지만 연산자 체인이 늘어나면 늘어날수록, 코드가 금방 **지저분해지게 됩니다**:

```javascript
import { take } from 'rxjs/operator/take';
import { map } from 'rxjs/operator/map';
import { of } from 'rxjs/observable/of';

map.call(
  take.call(
    of(1,2,3), 
    2
  ),
  val => val + 2
);
```

우리는 곧 이해할 수 없을 만큼 지저분한 코드를 가지게 될 수 있습니다. 어떻게 하면 양쪽의 장점을 다 가져갈 수 있을까요?

## Pipeable 연산자

RxJS는 이제  [`pipe`](https://github.com/ReactiveX/rxjs/blob/755df9bf908108974e38aaff79887279f2cde008/src/Observable.ts#L305-L329) 를 도입했습니다. 위에서 봤던 지저분한 코드를:

```javascript
import { take, map } from 'rxjs/operators';
import { of } from 'rxjs/observable/of';

map.call(
  take.call(
    of(1,2,3), 
    2
  ),
  val => val + 2
);
```

이렇게 바꿀 수 있습니다:

```javascript
import { take, map } from 'rxjs/operators';
import { of } from 'rxjs/observable/of';

of(1,2,3)
  .pipe(
    take(2),
    map(val => val + 2)
  );
```

더욱 읽기 쉬워졌죠? 이러한 방법은 애플리케이션의 RxJS 번들 사이즈를 줄여주는 효과도 가지고 있습니다. 더욱 자세히 알아보려면, [Ashwin Sureshkumar'의](https://twitter.com/Sureshkumar_Ash) 훌륭한 아티클인 Reduce Angular app bundle size using lettable operators](https://hackernoon.com/rxjs-reduce-bundle-size-using-lettable-operators-418307295e85) 를 읽어보세요.


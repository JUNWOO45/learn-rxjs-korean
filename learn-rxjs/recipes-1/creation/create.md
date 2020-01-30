# create

#### signature: `create(subscribe: function)`

## 주어진 subscription 함수로 옵저버블을 생성.

### 예시

**예시 1: 여러개의 값을 내보내는 옵저버블**

\( [StackBlitz](https://stackblitz.com/edit/typescript-baxh98?file=index.ts&devtoolsheight=100) \| [jsBin](http://jsbin.com/qorugiwaba/1/edit?js,console) \| [jsFiddle](https://jsfiddle.net/btroncone/td5107he/) \)

```javascript
// RxJS v6+
import { Observable } from 'rxjs';
/*
  subscription에서 'Hello' 와 'World'를 내보내는 옵저버블을 생성
*/
const hello = Observable.create(function(observer) {
  observer.next('Hello');
  observer.next('World');
  observer.complete();
});

//결과: 'Hello'...'World'
const subscribe = hello.subscribe(val => console.log(val));
```

**예시 2: 타이머에 맞춰서 짝수만 내보내는 옵저버블**

\( [StackBlitz](https://stackblitz.com/edit/typescript-xvezxn?file=index.ts&devtoolsheight=100) \| [jsBin](http://jsbin.com/lodilohate/1/edit?js,console) \| [jsFiddle](https://jsfiddle.net/btroncone/vtozg6uf/) \)

```javascript
// RxJS v6+
import { Observable } from 'rxjs';

/*
  매 1초마다 값을 증가시키고, 짝수만 내보낸다.
*/
const evenNumbers = Observable.create(function(observer) {
  let value = 0;
  const interval = setInterval(() => {
    if (value % 2 === 0) {
      observer.next(value);
    }
    value++;
  }, 1000);

  return () => clearInterval(interval);
});
//결과: 0...2...4...6...8
const subscribe = evenNumbers.subscribe(val => console.log(val));
//10초 후 unsubscribe
setTimeout(() => {
  subscribe.unsubscribe();
}, 10000);
```

### 추가 자료

* [create](http://reactivex.io/rxjs/class/es6/Observable.js~Observable.html#static-method-create) 📰 - 공식 문서
* [Creation operators: Create\(\)](https://egghead.io/lessons/rxjs-creation-operator-create?course=rxjs-beyond-the-basics-creating-observables-from-scratch) 📹 💵 - André Staltz
* [Using Observable.create for fine-grained control](https://egghead.io/lessons/rxjs-using-observable-create-for-fine-grained-control) 📹  💵 - Shane Osbourne

> 📂 Source Code: [https://github.com/ReactiveX/rxjs/blob/master/src/internal/observable/GenerateObservable.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/observable/GenerateObservable.ts)


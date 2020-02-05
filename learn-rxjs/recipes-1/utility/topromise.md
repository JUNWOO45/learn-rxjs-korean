# toPromise

#### signature: `toPromise() : Promise`

## 옵저버블을 프로미스로 바꾸어줍니다.

⚠ `toPromise` 는 옵저버블을 리턴하지 않기때문에, pipable 연산자가 아닙니다.

### 예시

**예시 1: 기본적인 프로미스**

\( [jsBin](http://jsbin.com/favoqecixi/1/edit?js,console) \| [jsFiddle](https://jsfiddle.net/btroncone/thykc9up/) \)

```javascript
//옵저버블을 리턴
const sample = val => Rx.Observable.of(val).delay(5000);
//옵저버블을 프로미스로 변환
const example = sample('First Example')
  .toPromise()
  //결과: 'First Example'
  .then(result => {
    console.log('From Promise:', result);
  });
```

**예시 2: Promise.all 사용**

\( [jsBin](http://jsbin.com/hutiyicaco/1/edit?js,console) \| [jsFiddle](https://jsfiddle.net/btroncone/xzu6u7hs/) \)

```javascript
// 옵저버블을 리턴
const sample = val => Rx.Observable.of(val).delay(5000);
/*
  각각을 프로미스로 바꾸고, Promise.all을 사용하여 모두 resolve되기를 기다립니다
*/
const example = () => {
  return Promise.all([
    sample('Promise 1').toPromise(),
    sample('Promise 2').toPromise()
  ]);
};
//결과: ["Promise 1", "Promise 2"]
example().then(val => {
  console.log('Promise.all Result:', val);
});
```

### 추가 자료

* [toPromise](https://github.com/Reactive-Extensions/RxJS/blob/master/doc/api/core/operators/topromise.md)📰 - 공식 문서

> 📂 Source Code: [https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/toPromise.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/toPromise.ts)


# toPromise

#### signature: `toPromise() : Promise`

## Convert observable to promise.

:warning: `toPromise` is not a pipable operator, as it does not return an observable.

### Examples

**Example 1: Basic Promise**

\( [jsBin](http://jsbin.com/favoqecixi/1/edit?js,console) \| [jsFiddle](https://jsfiddle.net/btroncone/thykc9up/) \)

```javascript
//return basic observable
const sample = val => Rx.Observable.of(val).delay(5000);
//convert basic observable to promise
const example = sample('First Example')
  .toPromise()
  //output: 'First Example'
  .then(result => {
    console.log('From Promise:', result);
  });
```

**Example 2: Using Promise.all**

\( [jsBin](http://jsbin.com/hutiyicaco/1/edit?js,console) \| [jsFiddle](https://jsfiddle.net/btroncone/xzu6u7hs/) \)

```javascript
//return basic observable
const sample = val => Rx.Observable.of(val).delay(5000);
/*
  convert each to promise and use Promise.all
  to wait for all to resolve
*/
const example = () => {
  return Promise.all([
    sample('Promise 1').toPromise(),
    sample('Promise 2').toPromise()
  ]);
};
//output: ["Promise 1", "Promise 2"]
example().then(val => {
  console.log('Promise.all Result:', val);
});
```

### Additional Resources

* [toPromise](https://github.com/Reactive-Extensions/RxJS/blob/master/doc/api/core/operators/topromise.md)

  :newspaper: - Official Docs

> :file\_folder: Source Code: [https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/toPromise.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/toPromise.ts)


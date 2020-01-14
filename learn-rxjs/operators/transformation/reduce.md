# reduce

#### signature: `reduce(accumulator: function, seed: any): Observable`

## Reduces the values from source observable to a single value that's emitted when the source completes.

:bulb: Just like [`Array.prototype.reduce()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce?v=a)

:bulb: If you need the current accumulated value on each emission, try [scan](scan.md)!

### Examples

**Example 1: Sum a stream of numbers**

\( [StackBlitz](https://stackblitz.com/edit/typescript-hdsv5e?file=index.ts&devtoolsheight=100) \| [jsBin](http://jsbin.com/dakuneneho/edit?js,console) \| [jsFiddle](https://jsfiddle.net/f8fw7yka/) \)

```javascript
// RxJS v6+
import { of } from 'rxjs';
import { reduce } from 'rxjs/operators';

const source = of(1, 2, 3, 4);
const example = source.pipe(reduce((acc, val) => acc + val));
//output: Sum: 10'
const subscribe = example.subscribe(val => console.log('Sum:', val));
```

### Additional Resources

* [reduce](https://rxjs.dev/api/operators/reduce)

  :newspaper: - Official docs

* [Scan\(\) vs reduce\(\) \| RxJS TUTORIAL](https://www.youtube.com/watch?v=myEeo2rZc3g)

  :video\_camera: - Academind

* [Build your own reduce operator](https://blog.strongbrew.io/build-the-operators-from-rxjs-from-scratch/?lectureId=reduce#app)

  :video\_camera: - Kwinten Pisman

> :file\_folder: Source Code: [https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/reduce.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/reduce.ts)


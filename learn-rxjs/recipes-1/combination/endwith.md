# endWith

#### signature: `endWith(an: Values): Observable`

## Emit given value\(s\) on completion.

:bulb: If you want to start with a value instead, check out [`startWith`](https://github.com/JUNWOO45/learn-rxjs-korean/tree/8c9661a5ef018c109eae0814410977d79cebac1b/operators/combination/startWith.md)!

:bulb: If you want to perform an action on completion, but do not want to emit a value, check out [`finalize`](../utility/finalize.md)!

### Examples

**Example 1: Basic endWith example**

\( [StackBlitz](https://stackblitz.com/edit/typescript-gexe9u?file=index.ts&devtoolsheight=100) \)

```javascript
// RxJS v6+
import { endWith } from 'rxjs/operators';
import { of } from 'rxjs';

const source$ = of('Hello', 'Friend', 'Goodbye');

source$
  // emit on completion
  .pipe(endWith('Friend'))
  // 'Hello', 'Friend', 'Goodbye', 'Friend'
  .subscribe(console.log(val));
```

**Example 2: endWith multiple values**

\( [StackBlitz](https://stackblitz.com/edit/typescript-dyed7x?file=index.ts&devtoolsheight=100) \)

```javascript
// RxJS v6+
import { endWith } from 'rxjs/operators';
import { of } from 'rxjs';

const source$ = of('Hello', 'Friend');

source$
  // emit on completion
  .pipe(endWith('Goodbye', 'Friend'))
  // 'Hello', 'Friend', 'Goodbye', 'Friend'
  .subscribe(console.log(val));
```

**Example 3: Comparison to finalize**

\( [StackBlitz](https://stackblitz.com/edit/typescript-lkk1pj?file=index.ts&devtoolsheight=100) \)

```javascript
// RxJS v6+
import { endWith, finalize } from 'rxjs/operators';
import { of } from 'rxjs';

const source$ = of('Hello', 'Friend');

source$
  // emit on completion
  .pipe(
    endWith('Goodbye', 'Friend'),
    // this function is invoked when unsubscribe methods are called
    finalize(() => console.log('Finally'))
  )
  // 'Hello', 'Friend', 'Goodbye', 'Friend'
  .subscribe(val => console.log(val));
// 'Finally'
```

### Additional Resources

* [endWith](https://rxjs.dev/api/operators/endWith)

  :newspaper: - Official docs

> :file\_folder: Source Code: [https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/endWith.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/endWith.ts)


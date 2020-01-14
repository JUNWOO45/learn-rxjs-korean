# Subject

## A special type of Observable which shares a single execution path among observers

### Examples

#### Example 1: simple Subject

\( [Stackblitz](https://stackblitz.com/edit/rxjs-subject-simple-example?file=index.ts&devtoolsheight=100) \)

```javascript
// RxJS v6+
import { Subject } from 'rxjs';

const sub = new Subject();

sub.next(1);
sub.subscribe(console.log);
sub.next(2); // OUTPUT => 2
sub.subscribe(console.log);
sub.next(3); // OUTPUT => 3,3 (logged from both subscribers)
```

### Related Recipes

* [Battleship Game](../recipes/battleship-game.md)
* [Lockscreen](../recipes/lockscreen.md)

### Additional Resources

* [Subject](https://rxjs-dev.firebaseapp.com/api/index/class/Subject)

  :newspaper: - Official docs

> :file\_folder: Source Code: [https://github.com/ReactiveX/rxjs/blob/master/src/internal/Subject.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/Subject.ts)


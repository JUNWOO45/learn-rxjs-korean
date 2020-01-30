# Type Ahead

_By_ [_adamlubek_](https://github.com/adamlubek)

This recipe demonstrates the creation of type ahead client side code.

## Example Code

\( [StackBlitz](https://stackblitz.com/edit/rxjs-type-ahead?file=index.ts&devtoolsheight=50) \)

![Typeahead](https://drive.google.com/uc?export=view&id=1TdDA78dkiy5lC8A3Rz28oDq9SuaxsS45)

```javascript
// RxJS v6+
import { fromEvent, of } from 'rxjs';
import {
  debounceTime,
  distinctUntilChanged,
  map,
  switchMap,
  tap
} from 'rxjs/operators';

const getContinents = keys =>
  [
    'africa',
    'antarctica',
    'asia',
    'australia',
    'europe',
    'north america',
    'south america'
  ].filter(e => e.indexOf(keys.toLowerCase()) > -1);

const fakeContinentsRequest = keys =>
  of(getContinents(keys)).pipe(
    tap(_ => console.log(`API CALL at ${new Date()}`))
  );

fromEvent(document.getElementById('type-ahead'), 'keyup')
  .pipe(
    debounceTime(200),
    map((e: any) => e.target.value),
    distinctUntilChanged(),
    switchMap(fakeContinentsRequest),
    tap(c => (document.getElementById('output').innerText = c.join('\n')))
  )
  .subscribe();
```

### html

```markup
Get continents
<input id="type-ahead" />
<hr />
<div id="output"></div>
```

## Operators Used

* [debounceTime](../recipes-1/filtering/debouncetime.md)
* [distinctUntilChanged](../recipes-1/filtering/distinctuntilchanged.md)
* [fromEvent](../recipes-1/creation/fromevent.md)
* [map](../recipes-1/transformation/map.md)
* [of](../recipes-1/creation/of.md)
* [switchMap](../recipes-1/transformation/switchmap.md)
* [tap](../recipes-1/utility/do.md)


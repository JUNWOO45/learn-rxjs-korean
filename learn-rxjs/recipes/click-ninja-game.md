# Click Ninja Game

_By_ [_adamlubek_](https://github.com/adamlubek)

This recipe shows usage of time interval operator in a simple game

## Example Code

\( [StackBlitz](https://stackblitz.com/edit/rxjs-click-ninja?file=index.ts) \)

![Click Ninja Game](https://drive.google.com/uc?export=view&id=1VT8umN-jtaqBfcKtlCwZ3w805qe3bXWN)

### index.ts

```javascript
// RxJS v6+
import { fromEvent, TimeInterval } from 'rxjs';
import { timeInterval, takeWhile, scan, tap, repeat, finalize } from 'rxjs/operators';
import { render, clear } from './html-renderer';

interface State {
  score: number;
  interval: number;
  threshold: number;
}

fromEvent(document, 'mousedown').pipe(
  timeInterval(),
  scan<TimeInterval<Event>, State>((state, timeInterval) => ({
    score: state.score + 1,
    interval: timeInterval.interval,
    threshold: state.threshold - 2
  }), { score: 0, interval: 0, threshold: 300 }),
  takeWhile((state: State) => state.interval < state.threshold),
  tap((state: State) => render(state.score, Math.floor(state.score / 10))),
  finalize(clear),
  repeat()
).subscribe();
```

### html-renderer.ts

```javascript
const texts = {
  0: 'click, click',
  1: 'keep clicking',
  2: 'wow',
  3: 'not tired yet?!',
  4: 'click master!',
  5: 'inhuman!!!',
  6: 'ininhuman!!!'
};

const text = (score: number, level: number) => `${texts[level]} \n ${score}`;

export const render = (score: number, level: number) => {
  const id = 'level' + level;
  const element = document.getElementById(id);
  const innerText = text(score, level);
  if (element) {
    element.innerText = innerText;
  } else {
    const elem = document.createElement('div');
    elem.id = id;
    elem.style.zIndex = `${level}`;
    elem.style.position = 'absolute';
    elem.style.height = '150px';
    elem.style.width = '150px';
    elem.style.borderRadius = '10px';
    const position = level * 20;
    elem.style.top = position + 'px';
    elem.style.left = position + 'px';
    const col = 100 + position;
    elem.style.background = `rgb(0,${col},0)`;
    elem.style.color = 'white';
    elem.innerText = innerText;
    elem.style.textAlign = 'center';
    elem.style.verticalAlign = 'middle';
    elem.style.lineHeight = '90px';
    document.body.appendChild(elem);
  }
};

export const clear = () => (document.body.innerText = '');
```

#### html

```text
<div>How fast can you click?!</div>
```

* [finalize](../recipes-1/utility/finalize.md)
* [fromEvent](../recipes-1/creation/fromevent.md)
* [repeat](../recipes-1/utility/repeat.md)
* [scan](../recipes-1/transformation/scan.md)
* [takeWhile](../recipes-1/filtering/takewhile.md)
* [tap](../recipes-1/utility/do.md)
* [timeInterval](../recipes-1/utility/timeinterval.md)


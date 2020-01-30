# fromEvent

#### signature: `fromEvent(target: EventTargetLike, eventName: string, selector: function): Observable`

## 이벤트를 옵저버블로 전환해줍니다.

### 예시

**예시 1: 마우스 클릭을 옵저버블로 전환**

\( [StackBlitz](https://stackblitz.com/edit/typescript-mfyefr?file=index.ts&devtoolsheight=50) \| [jsBin](http://jsbin.com/xikapewoqa/1/edit?js,console,output) \| [jsFiddle](https://jsfiddle.net/btroncone/vbLz1pdx/) \)

```javascript
// RxJS v6+
import { fromEvent } from 'rxjs';
import { map } from 'rxjs/operators';

// 클릭 이벤트를 내보내는 옵저버블을 생성합니다
const source = fromEvent(document, 'click');
//주어진 이벤트 타임스탬프를 사용하여 문자열에 맵핑합니다
const example = source.pipe(map(event => `Event time: ${event.timeStamp}`));
//결과 (예시): 'Event time: 7276.390000000001'
const subscribe = example.subscribe(val => console.log(val));
```

### 관련된 사용법

* [Alphabet Invasion Game](../../recipes/alphabet-invasion-game.md)
* [Battleship Game](../../recipes/battleship-game.md)
* [Breakout Game](../../recipes/breakout-game.md)
* [Car Racing Game](../../recipes/car-racing-game.md)
* [Catch The Dot Game](../../recipes/catch-the-dot-game.md)
* [Click Ninja Game](../../recipes/click-ninja-game.md)
* [Flappy Bird Game](../../recipes/flappy-bird-game.md)
* [Game Loop](../../recipes/gameloop.md)
* [Horizontal Scroll Indicator](../../recipes/horizontal-scroll-indicator.md)
* [HTTP Polling](../../recipes/http-polling.md)
* [Lockscreen](../../recipes/lockscreen.md)
* [Memory Game](../../recipes/memory-game.md)
* [Mine Sweeper Game](../../recipes/mine-sweeper-game.md)
* [Platform Jumper Game](../../recipes/platform-jumper-game.md)
* [Progress Bar](../../recipes/progressbar.md)
* \[Save Indicator\]\('../../recipes/save-indicator.md\)
* [Smart Counter](../../recipes/smartcounter.md)
* [Space Invaders Game](../../recipes/space-invaders-game.md)
* [Stop Watch](../../recipes/stop-watch.md)
* [Swipe To Refresh](../../recipes/swipe-to-refresh.md)
* [Tank Battle Game](../../recipes/tank-battle-game.md)
* [Tetris Game](../../recipes/tetris-game.md)
* [Type Ahead](../../recipes/type-ahead.md)
* [Uncover Image Game](../../recipes/uncover-image-game.md)

### 추가 자료

* [fromEvent](https://rxjs.dev/api/index/function/fromEvent)

  :newspaper: - 공식 문서

> :file\_folder: Source Code: [https://github.com/ReactiveX/rxjs/blob/master/src/internal/observable/fromEvent.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/observable/fromEvent.ts)


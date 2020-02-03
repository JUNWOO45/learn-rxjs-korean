# finalize / finally

#### signature: `finalize(callback: () => void)`

## 옵저버블이 완료되거나 에러 발생 시 함수를 호출합니다

### 예시

**예시 1: 옵저버블이 완료될 때 콜백 함수를 실행시킵니다**

\( [StackBlitz](https://stackblitz.com/edit/typescript-ohddud) \)

```javascript
import { interval } from 'rxjs';
import { take, finalize } from 'rxjs/operators';

//매 1초 마다 값을 발생시킵니다
const source = interval(1000);
//결과: 0,1,2,3,4,5....
const example = source.pipe(
  take(5), //첫 5개의 값만 받습니다
  finalize(() => console.log('Sequence complete')) // 옵저버블이 완료되면, 콜백함수를 실행시킵니다
)
const subscribe = example.subscribe(val => console.log(val));
```

### 관련된 사용법

* [Battleship Game](../../recipes/battleship-game.md)
* [Car Racing Game](../../recipes/car-racing-game.md)
* [Click Ninja Game](../../recipes/click-ninja-game.md)
* [HTTP Polling](../../recipes/http-polling.md)
* [Mine Sweeper Game](../../recipes/mine-sweeper-game.md)
* [Swipe To Refresh](../../recipes/swipe-to-refresh.md)
* [Tetris Game](../../recipes/tetris-game.md)

### 추가 자료

* [finalize](https://rxjs.dev/api/operators/finalize)

  :newspaper: - 공식 문서

> :file\_folder: Source Code: [https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/finalize.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/finalize.ts)


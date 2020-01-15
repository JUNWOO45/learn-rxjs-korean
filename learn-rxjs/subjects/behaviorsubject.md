# BehaviorSubject

## 초기값이 필요하며 현재 값을 새로운 subscribers에게 전달한다

:bulb: 구독 시 마지막 값을 전달하고 싶지만, 초기값을 제공하지 않으려면, [ReplaySubject](replaysubject.md)를 살펴보세요.

### 예시

#### 예시1: 간단한 BehaviorSubject

\( [Stackblitz](https://stackblitz.com/edit/rxjs-behaviorsubject-simpleexample?file=index.ts?file=index.ts&devtoolsheight=100) \)

```javascript
// RxJS v6+
import { BehaviorSubject } from 'rxjs';

const subject = new BehaviorSubject(123);

// 두개의 새로운 subscriber는 초기값을 받습니다 => 결과: 123, 123
subject.subscribe(console.log);
subject.subscribe(console.log);

// 두 subscriber는 새로운 값을 받습니다 => 결과: 456, 456
subject.next(456);

// 새로운 subscriber는 마지막 값을 받습니다 (456) => 결과: 456
subject.subscribe(console.log);

// 위 3개의 subscriber는 새로운 값을 받습니다 => 결과: 789, 789, 789
subject.next(789);

// 결과: 123, 123, 456, 456, 456, 789, 789, 789
```

#### 예시 2: 마우스 클릭으로 만들어진 새로운 subscriber와 BehaviorSubject

\( [Stackblitz](https://stackblitz.com/edit/rxjs-behaviorsubject-mouseclicks?file=index.ts) \)

```javascript
// RxJS v6+
import { BehaviorSubject, fromEvent, interval, merge } from 'rxjs';
import { map, tap, mergeMap } from 'rxjs/operators';

const setElementText = (elemId, text) =>
  (document.getElementById(elemId).innerText = text.toString());
const addHtmlElement = coords =>
  (document.body.innerHTML += `
  <div 
    id=${coords.id}
    style="
      position: absolute;
      height: 30px;
      width: 30px;
      text-align: center;
      top: ${coords.y}px;
      left: ${coords.x}px;
      background: silver;
      border-radius: 80%;"
    >
  </div>`);

const subject = new BehaviorSubject(0);

const click$ = fromEvent(document, 'click').pipe(
  map((e: MouseEvent) => ({
    x: e.clientX,
    y: e.clientY,
    id: Math.random()
  })),
  tap(addHtmlElement),
  mergeMap(coords => subject.pipe(tap(v => setElementText(coords.id, v))))
);

const interval$ = interval(1000).pipe(
  tap(v => subject.next(v)),
  tap(v => setElementText('intervalValue', v))
);

merge(click$, interval$).subscribe();
```

### 관련한 사용법

* [Alphabet Invasion Game](../recipes/alphabet-invasion-game.md)
* [Battleship Game](../recipes/battleship-game.md)
* [Car Racing Game](../recipes/car-racing-game.md)

### 추가 자료

* [BehaviorSubject](https://rxjs-dev.firebaseapp.com/api/index/class/BehaviorSubject)

  :newspaper: - 공식 문서

> :file\_folder: 소스 코드: [https://github.com/ReactiveX/rxjs/blob/master/src/internal/BehaviorSubject.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/BehaviorSubject.ts)


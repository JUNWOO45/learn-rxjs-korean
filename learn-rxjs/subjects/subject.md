# Subject

## 옵저버 간 단일 실행 경로를 공유하는 특별한 유형의 옵저버블

### 예시

#### 예시 1: 간단한 Subject

\( [Stackblitz](https://stackblitz.com/edit/rxjs-subject-simple-example?file=index.ts&devtoolsheight=100) \)

```javascript
// RxJS v6+
import { Subject } from 'rxjs';

const sub = new Subject();

sub.next(1);
sub.subscribe(console.log);
sub.next(2); // 결과 => 2
sub.subscribe(console.log);
sub.next(3); // 결과 => 3,3 (양쪽의 subscribers로부터 로그가 찍힌다)
```

### 관련된 사용법

* [Battleship Game](../recipes/battleship-game.md)
* [Lockscreen](../recipes/lockscreen.md)

### 추가 자료

* [Subject](https://rxjs-dev.firebaseapp.com/api/index/class/Subject) 📰 - 공식 문서

> 📂 Source Code: [https://github.com/ReactiveX/rxjs/blob/master/src/internal/Subject.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/Subject.ts)


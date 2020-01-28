# ReplaySubject

## "재생"하거나 새로운 subscribers에게 이전 값 전송

### 예시

#### 예시 1: 간단한 ReplaySubject

\( [Stackblitz](https://stackblitz.com/edit/rxjs-replaysubject-simple-example?file=index.ts&devtoolsheight=100) \)

```javascript
// RxJS v6+
import { ReplaySubject } from 'rxjs';

const sub = new ReplaySubject(3);

sub.next(1);
sub.next(2);
sub.subscribe(console.log); // 결과 => 1,2
sub.next(3); // 결과 => 3
sub.next(4); // 결과 => 4
sub.subscribe(console.log); // 결과 => 2,3,4 (새로운 subscriber의 최근 3개 값 로그)
sub.next(5); // OUTPUT => 5,5 (양쪽 subscribers의 로그)
```

### 추가 자료

* [ReplaySubject](https://rxjs-dev.firebaseapp.com/api/index/class/ReplaySubject) 📰 - 공식 문서


> 📂 Source Code: [https://github.com/ReactiveX/rxjs/blob/master/src/internal/ReplaySubject.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/ReplaySubject.ts)


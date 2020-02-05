# dematerialize

#### signature: `dematerialize(): Observable`

## 알림\(notification\) 객체를 값으로 바꾸어줍니다.

### 예시

**예시 1: notifications를 값으로 바꾸어줍니다**

\( [StackBlitz](https://stackblitz.com/edit/typescript-bxdwbg?file=index.ts&devtoolsheight=100) \| [jsBin](http://jsbin.com/vafedocibi/1/edit?js,console) \| [jsFiddle](https://jsfiddle.net/btroncone/jw08mouy/) \)

```javascript
// RxJS v6+
import { from, Notification } from 'rxjs';
import { dematerialize } from 'rxjs/operators';

//next와 error 알림을 내보냅니다
const source = from([
  Notification.createNext('SUCCESS!'),
  Notification.createError('ERROR!')
]).pipe(
  //알림 객체를 알림 값으로 바꾸어줍니다
  dematerialize()
);

//결과: 'NEXT VALUE: SUCCESS' 'ERROR VALUE: 'ERROR!'
const subscription = source.subscribe({
  next: val => console.log(`NEXT VALUE: ${val}`),
  error: val => console.log(`ERROR VALUE: ${val}`)
});
```

### 추가 자료

* [dematerialize](https://rxjs.dev/api/operators/dematerialize) 📰 - 공식 문서

> 📂 Source Code: [https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/demterialize.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/dematerialize.ts)


# 시간 기반의 연산자 비교

RxJS는 풍부한 양의 시간을 다루는 연산자를 제공하지만, 이러한 다양성은 종종 사용하려는 연산자가 적합한 연산자가 맞는지 헷갈리게 합니다. 빈번하게 사용되는 시간 연산자들을 시각화하여 비교해봅시다.

비교할 연산자:

* [auditTime](../recipes-1/filtering/audittime.md)
* [bufferTime](../recipes-1/transformation/buffertime.md)
* [debounceTime](../recipes-1/filtering/debouncetime.md)
* sampleTime
* [throttleTime](../recipes-1/filtering/throttletime.md)

\( [Stackblitz](https://stackblitz.com/edit/rxjs-time-based-operators-comparison?file=index.ts&devtoolsheight=100)\)

```javascript
/*
interval      ^0-------1-------2-------3-------4-------5-------6-------7-------8-------9------|
auditTime     ^------------------------3-------------------------------7----------------------|
bufferTime    ^----------------[0,1]-------------------[2,3,4]-----------------[5,6,7]-[8,9]--|
debounceTime  ^------------------------------------------------------------------------9------|
sampleTime    ^----------------1-----------------------4-----------------------7--------------|
throttleTime  ^0-------------------------------4-------------------------------8--------------|
*/

// RxJS v6+
import { interval, merge } from 'rxjs';
import { auditTime, bufferTime, debounceTime, sampleTime, throttleTime, tap, take } from 'rxjs/operators';

const takeValue = 10;
const intrvl = 1000;
const time = 3000;

const intervaled = (operator, operatorName) =>
  interval(intrvl)
    .pipe(
      take(takeValue),
      operator,
      tap(x => console.log(`${operatorName}:${x}`))
    );

merge(
  interval(intrvl).pipe(take(takeValue), tap(v => console.log(`i: ${v}`))),
  intervaled(auditTime(time), "auditTime"),
  intervaled(bufferTime(time), "bufferTime"),
  intervaled(debounceTime(time), "debounceTime"),
  intervaled(sampleTime(time), "sampleTime"),
  intervaled(throttleTime(time), "throttleTime")
).subscribe();

// 결과
/*
0
throttleTime:0
1
2
bufferTime:0,1
sampleTime:1
3
auditTime:3
4
throttleTime:4
5
bufferTime:2,3,4
sampleTime:4
6
7
auditTime:7
8
bufferTime:5,6,7
sampleTime:7
throttleTime:8
9
bufferTime:8,9
debounceTime:9

*/
```


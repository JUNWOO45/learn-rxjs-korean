# Subjects

Subject는 옵저버들 간에 단일 실행 경로를 공유하는 특별한 유형의 옵저버블입니다.

사람들로 가득 찬 방에서 마이크를 들고 말하는 단 한 명의 사람으로 생각할 수 있습니다. 그들의 메시지 \(the subject\) 는 수많은 \(multicast\) 사람들에게 \(the observers\) 동시에 전달됩니다. 멀티캐스팅**의 개념입니다. 일반적인 옵저버블은 1대 1의 대화라고 생각할 수 있습니다.

subjects에는 4가지 종류가 있습니다:

* **Subject** - 초기값과 전달하려는 동작이 없다.
* **AsyncSubject** - complete(완료)되면 마지막 이벤트를 발생한다.
* **BehaviorSubject** - 초기값이 필요하며 현재 값(마지막으로 내보낸 항목)을 새로운 subscribers에게 전달한다.
* **ReplaySubject** - 새로운 subscribers에게 저장된 모든 값들을 전달한다.

## 목차

* [AsyncSubject](asyncsubject.md)
* [BehaviorSubject](behaviorsubject.md)
* [ReplaySubject](replaysubject.md)
* [Subject](subject.md)

## Subjects 비교

\( [Stackblitz](https://stackblitz.com/edit/rxjs-subjects-comparison?file=index.ts&devtoolsheight=100) \)

```javascript
/*
                   s1    n(r)   n(x)    s2     n(j)   c    n(s)
Subject            
        s1         ^-----r------x--------------j------|----------
        s2         ---------------------^------j------|----------
AsyncSubject       
        s1         ^----------------------------------j|---------
        s2         ---------------------^-------------j|---------
BehaviorSubject    
        s1         ^a----r------x--------------j------|----------
        s2         ---------------------^x-----j------|----------
ReplaySubject      
        s1         ^-----r------x--------------j------|----------
        s2         ---------------------^r-x---j------|----------
*/

// RxJS v6+
import { Subject, AsyncSubject, BehaviorSubject, ReplaySubject } from 'rxjs';

const subject = new Subject();
const asyncSubject = new AsyncSubject();
const behaviorSubject = new BehaviorSubject('a');
const replaySubject = new ReplaySubject(2);

const subjects = [subject, asyncSubject, behaviorSubject, replaySubject];
const log = subjectType => e => console.log(`${subjectType}: ${e}`);

console.log('SUBSCRIBE 1');
subject.subscribe(log('s1 subject'));
asyncSubject.subscribe(log('s1 asyncSubject'));
behaviorSubject.subscribe(log('s1 behaviorSubject'));
replaySubject.subscribe(log('s1 replaySubject'));

console.log('\nNEXT(r)');
subjects.forEach(o => o.next('r'));

console.log('\nNEXT(x)');
subjects.forEach(o => o.next('x'));

console.log('\nSUBSCRIBE 2');
subject.subscribe(log('s2 subject'));
asyncSubject.subscribe(log('s2 asyncSubject'));
behaviorSubject.subscribe(log('s2 behaviorSubject'));
replaySubject.subscribe(log('s2 replaySubject'));

console.log('\nNEXT(j)');
subjects.forEach(o => o.next('j'));

console.log('\nCOMPLETE');
subjects.forEach(o => o.complete());

console.log('\nNEXT(s)');
subjects.forEach(o => o.next('s'));

/*
OUTPUT:

SUBSCRIBE 1
s1 behaviorSubject: a

NEXT(r)
s1 subject: r
s1 behaviorSubject: r
s1 replaySubject: r

NEXT(x)
s1 subject: x
s1 behaviorSubject: x
s1 replaySubject: x

SUBSCRIBE 2
s2 behaviorSubject: x
s2 replaySubject: r
s2 replaySubject: x

NEXT(j)
s1 subject: j
s2 subject: j
s1 behaviorSubject: j
s2 behaviorSubject: j
s1 replaySubject: j
s2 replaySubject: j

COMPLETE
s1 asyncSubject: j
s2 asyncSubject: j

NEXT(s)
*/
```

### 추가 자료

* [공식 개요](http://reactivex.io/rxjs/manual/overview.html#subject)

  :newspaper:

* [공식 문서](http://reactivex.io/documentation/subject.html)

  :newspaper:

* [On The Subject Of Subjects \(in RxJS\)](https://medium.com/@benlesh/on-the-subject-of-subjects-in-rxjs-2b08b7198b93)

  :newspaper: - Ben Lesh


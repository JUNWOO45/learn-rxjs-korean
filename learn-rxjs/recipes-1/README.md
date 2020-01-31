# 연산자

명확한 설명, 관련된 자료 및 예제가 수록된 RxJS 연산자 목록

[_알파벳 순서로 보고 싶으신가요?_](complete.md)

## 목차 \(연산자 타입으로 분류\)

* [Combination](combination/)
  * [combineAll](combination/combineall.md)
  * [combineLatest](combination/combinelatest.md) :star:
  * [concat](combination/concat.md) :star:
  * [concatAll](combination/concatall.md)
  * [endWith](combination/endwith.md)
  * [forkJoin](combination/forkjoin.md)
  * [merge](combination/merge.md) :star:
  * [mergeAll](combination/mergeall.md)
  * [pairwise](combination/pairwise.md)
  * [race](combination/race.md)
  * [startWith](combination/startwith.md) :star:
  * [withLatestFrom](combination/withlatestfrom.md) :star:
  * [zip](combination/zip.md)
* [Conditional](conditional/)
  * [defaultIfEmpty](conditional/defaultifempty.md)
  * [every](conditional/every.md)
  * [iif](conditional/iif.md)
  * [sequenceequal](conditional/sequenceequal.md)
* [Creation](creation/)
  * [ajax](creation/ajax.md) :star:
  * [create](creation/create.md)
  * [defer](creation/defer.md)
  * [empty](creation/empty.md)
  * [from](creation/from.md) :star:
  * [fromEvent](creation/fromevent.md)
  * [generate](creation/generate.md)
  * [interval](creation/interval.md)
  * [of](creation/of.md) :star:
  * [range](creation/range.md)
  * [throw](creation/throw.md)
  * [timer](creation/timer.md)
* [Error Handling](error_handling/)
  * [catch / catchError](error_handling/catch.md) :star:
  * [retry](error_handling/retry.md)
  * [retryWhen](error_handling/retrywhen.md)
* [Filtering](filtering/)
  * [audit](filtering/audit.md)
  * [auditTime](filtering/audittime.md)
  * [debounce](filtering/debounce.md)
  * [debounceTime](filtering/debouncetime.md) :star:
  * [distinct](filtering/distinct.md)
  * [distinctUntilChanged](filtering/distinctuntilchanged.md) :star:
  * [distinctUntilKeyChanged](https://github.com/JUNWOO45/learn-rxjs-korean/tree/8c9661a5ef018c109eae0814410977d79cebac1b/operators/distinctuntilkeychanged.md)
  * [filter](filtering/filter.md) :star:
  * [find](filtering/find.md)
  * [first](filtering/first.md)
  * [ignoreElements](filtering/ignoreelements.md)
  * [last](filtering/last.md)
  * [sample](filtering/sample.md)
  * [single](filtering/single.md)
  * [skip](filtering/skip.md)
  * [skipUntil](filtering/skipuntil.md)
  * [skipWhile](filtering/skipwhile.md)
  * [take](filtering/take.md) :star:
  * [takeLast](filtering/takelast.md)
  * [takeUntil](filtering/takeuntil.md) :star:
  * [takeWhile](filtering/takewhile.md)
  * [throttle](filtering/throttle.md)
  * [throttleTime](filtering/throttletime.md)
* [Multicasting](multicasting/)
  * [multicast](multicasting/multicast.md)
  * [publish](multicasting/publish.md)
  * [share](multicasting/share.md) :star:
  * [shareReplay](multicasting/sharereplay.md) :star:
* [Transformation](transformation/)
  * [buffer](transformation/buffer.md)
  * [bufferCount](transformation/buffercount.md)
  * [bufferTime](transformation/buffertime.md) :star:
  * [bufferToggle](transformation/buffertoggle.md)
  * [bufferWhen](transformation/bufferwhen.md)
  * [concatMap](transformation/concatmap.md) :star:
  * [concatMapTo](transformation/concatmapto.md)
  * [expand](transformation/expand.md)
  * [exhaustMap](transformation/exhaustmap.md)
  * [groupBy](transformation/groupby.md)
  * [map](transformation/map.md) :star:
  * [mapTo](transformation/mapto.md)
  * [mergeMap / flatMap](transformation/mergemap.md) :star:
  * [mergeScan](transformation/mergescan.md)
  * [partition](transformation/partition.md)
  * [pluck](transformation/pluck.md)
  * [reduce](transformation/reduce.md)
  * [scan](transformation/scan.md) :star:
  * [switchMap](transformation/switchmap.md) :star:
  * [switchMapTo](transformation/switchmapto.md)
  * [toArray](transformation/toarray.md)
  * [window](transformation/window.md)
  * [windowCount](transformation/windowcount.md)
  * [windowTime](transformation/windowtime.md)
  * [windowToggle](transformation/windowtoggle.md)
  * [windowWhen](transformation/windowwhen.md)
* [Utility](utility/)
  * [tap / do](utility/do.md) :star:
  * [delay](utility/delay.md)
  * [delayWhen](utility/delaywhen.md)
  * [dematerialize](utility/dematerialize.md)
  * [finalize / finally](utility/finalize.md)
  * [let](utility/let.md)
  * [repeat](utility/repeat.md)
  * [repeatWhen](https://github.com/JUNWOO45/learn-rxjs-korean/tree/8c9661a5ef018c109eae0814410977d79cebac1b/operators/utility/repeatwhen.md)
  * [timeInterval](utility/timeinterval.md)
  * [timeout](utility/timeout.md)
  * [timeoutWith](utility/timeoutwith.md)
  * [toPromise](utility/topromise.md)

:star: - _자주 사용되는 연산자_

## 추가 자료

* [What Are Operators?](http://reactivex.io/rxjs/manual/overview.html#operators)

  :newspaper: - 공식 문서

* [What Operators Are](https://egghead.io/lessons/rxjs-what-rxjs-operators-are)

  :video\_camera: :dollar: - André Staltz


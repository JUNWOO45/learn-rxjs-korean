# RxJS 배우기

## RxJS 배우기

RxJS에 대한 명확한 예제, 설명, 그리고 자료

_By_ [_@btroncone_](https://twitter.com/BTroncone)

## 소개

[RxJS](https://github.com/ReactiveX/rxjs)는 오늘날 웹 개발에서 가장 인기있는 라이브러리 중 하나입니다. 이벤트를 다루거나, 수많은 프레임워크, 라이브러리, 유틸리티 등에 모두 사용가능한 강력한 함수형 접근방식때문에, 더 많은 사람들이 Rx를 배우고 있습니다.  리액티브 프로그래밍, 그리고 이 Rx의 기능에 대한 확실한 이해를 가지고 있다면, 여러분은 [대부분의 언어](http://reactivex.io/languages.html)에서 Rx를 사용할 수 있습니다.

**하지만...**

RxJS와 리액티브 프로그래밍을 배우는 것은 [어렵습니다](https://twitter.com/hoss/status/742643506536153088). [명령형과 선언형 프로그래밍](https://tylermcginnis.com/imperative-vs-declarative-programming/)에서부터 수많은 개념들, 다양한 API, 근본적인 사고방식의 변화에 이르기까지 많은 것들을 배워야합니다. 이 사이트는 RxJS에 관한 이해하기 쉬운 설명, 깔끔한 예제와 간단한 검색, 그리고 웹 상에 존재하는 좋은 참고자료들을 제공하고 있습니다. 이 사이트는 새롭고 신선한 관점을 제공하여 배우기 힘들고 고통스러웠던 [공식 문서](http://reactivex.io/rxjs/)와 기존의 학습자료들을 보충하려합 Rx를 배우는 것은 어려울테지만, 확실히 노력할 가치가 있습니다!

### RxJS가 처음이신가요?

[RxJS 입문서](learn-rxjs/concepts/rxjs-primer.md)를 통해 생산성을 높이는 데 필요한 모든 핵심 개념들을 학습하세요!

## 목차

#### Operators(연산자)

Operators(연산자)는 복잡한 비동기 작업을 우아하고 선언적인 솔루션으로 해결해주는 강력한 기술입니다. 이번 섹션은 모든  [RxJS 연산자](learn-rxjs/operators/)와 실행 가능한 명확한 예제를 함께 포함하고 있습니다 . 추가 자료와 각각의 연산자에대한 적절한 사용법 또한 제공되고 있습니다.

**Operator(연산자) 카테고리**

* [Combination](learn-rxjs/operators/combination/)
* [Conditional](learn-rxjs/operators/conditional/)
* [Creation](learn-rxjs/operators/creation/)
* [Error Handling](learn-rxjs/operators/error_handling/)
* [Multicasting](learn-rxjs/operators/multicasting/)
* [Filtering](learn-rxjs/operators/filtering/)
* [Transformation](learn-rxjs/operators/transformation/)
* [Utility](learn-rxjs/operators/utility/)

**혹은...**

[알파벳 순으로 나열](learn-rxjs/operators/complete.md)

#### Subjects 이해하기

Subject는 옵저버들 간에 단일 실행 경로를 공유하는 특별한 유형의 옵저버블입니다.

* [개요](learn-rxjs/subjects/)
* [AsyncSubject](learn-rxjs/subjects/asyncsubject.md)
* [BehaviorSubject](learn-rxjs/subjects/behaviorsubject.md)
* [ReplaySubject](learn-rxjs/subjects/replaysubject.md)
* [Subject](learn-rxjs/subjects/subject.md)

#### 개념

옵저버블이 어떻게 동작하는지에 대한 확실한 기초 지식이 없다면, RxJS가 '마법'으로 느껴질겁니다. 이번 섹션에서는 리액티브 프로그래밍, 그리고 옵저버블과 친해지기위해 필요한 중요한 개념들을 익히게 됩니다.

* [RxJS Primer](learn-rxjs/concepts/rxjs-primer.md)
* [RxJS v5 -&gt; v6 Upgrade](learn-rxjs/concepts/rxjs5-6.md)
* [Time based operators comparison](learn-rxjs/concepts/time-based-operators-comparison.md)
* [Understanding Operator Imports](learn-rxjs/concepts/operator-imports.md)

#### 사용법

RxJS를 사용한 일반적인 예시 및 흥미로운 사용법들.

* [Alphabet Invasion Game](learn-rxjs/recipes/alphabet-invasion-game.md)
* [Battleship Game](learn-rxjs/recipes/battleship-game.md)
* [Breakout Game](learn-rxjs/recipes/breakout-game.md)
* [Car Racing Game](learn-rxjs/recipes/car-racing-game.md)
* [Catch The Dot Game](learn-rxjs/recipes/catch-the-dot-game.md)
* [Click Ninja Game](learn-rxjs/recipes/click-ninja-game.md)
* [Flappy Bird Game](learn-rxjs/recipes/flappy-bird-game.md)
* [Game Loop](learn-rxjs/recipes/gameloop.md)
* [Horizontal Scroll Indicator](learn-rxjs/recipes/horizontal-scroll-indicator.md)
* [HTTP Polling](learn-rxjs/recipes/http-polling.md)
* [Lockscreen](learn-rxjs/recipes/lockscreen.md)
* [Matrix Digital Rain](learn-rxjs/recipes/matrix-digital-rain.md)
* [Memory Game](learn-rxjs/recipes/memory-game.md)
* [Mine Sweeper Game](learn-rxjs/recipes/mine-sweeper-game.md)
* [Platform Jumper Game](learn-rxjs/recipes/platform-jumper-game.md)
* [Progress Bar](learn-rxjs/recipes/progressbar.md)
* [Save Indicator](learn-rxjs/recipes/save-indicator.md)
* [Smart Counter](learn-rxjs/recipes/smartcounter.md)
* [Stop Watch](learn-rxjs/recipes/stop-watch.md)
* [Space Invaders Game](learn-rxjs/recipes/space-invaders-game.md)
* [Swipe To Refresh](learn-rxjs/recipes/swipe-to-refresh.md)
* [Tank Battle Game](learn-rxjs/recipes/tank-battle-game.md)
* [Tetris Game](learn-rxjs/recipes/tetris-game.md)
* [Type Ahead](learn-rxjs/recipes/type-ahead.md)
* [Uncover Image Game](learn-rxjs/recipes/uncover-image-game.md)

## 입문자들을 위한 자료

RxJS와 리액티브 프로그래밍을 처음 접하십니까? 이 사이트에서 찾을 수 있는 콘텐츠 외에도, 아래의 자료들은 여러분의 학습에 큰 도움을 줄 것입니다.

#### 컨퍼런스

* [RxJS Live](https://www.rxjs.live/) - RxJS specific conference, Las Vegas

#### 읽을거리

* [RxJS Introduction](https://rxjs-dev.firebaseapp.com/guide/overview) - 공식문서

* [The Introduction to Reactive Programming You've Been Missing](https://gist.github.com/staltz/868e7e9bc2a7b8c1f754) - André Staltz

* [RxJS: Observables, Observers and Operators Introduction](https://ultimatecourses.com/blog/rxjs-observables-observers-operators) - Todd Motto

#### 영상

* [RxJS Basics](https://ultimatecourses.com/courses/rxjs?ref=4) :dollar: - Brian Troncone

* [Asynchronous Programming: The End of The Loop](https://egghead.io/courses/mastering-asynchronous-programming-the-end-of-the-loop) - Jafar Husain

* [What is RxJS?](https://egghead.io/lessons/rxjs-what-is-rxjs) - Ben Lesh
* [Creating Observable from Scratch](https://egghead.io/lessons/rxjs-creating-observable-from-scratch) - Ben Lesh

* [Introduction to RxJS Marble Testing](https://egghead.io/lessons/rxjs-introduction-to-rxjs-marble-testing) :dollar: - Brian Troncone

* [Introduction to Reactive Programming](https://egghead.io/courses/introduction-to-reactive-programming) :dollar: - André Staltz

* [Reactive Programming using Observables](https://www.youtube.com/watch?v=HT7JiiqnYYc&feature=youtu.be) - Jeremy Lund

#### 예제

* [Functional Programming in JavaScript](http://reactivex.io/learnrx/) - Jafar Husain

#### 도구들

* [Rx Marbles - Interactive diagrams of Rx Observables](http://rxmarbles.com/) - André Staltz

* [Rx Visualizer - Animated playground for Rx Observables](https://rxviz.com) - Misha Moroshko

* [Reactive.how - Animated cards to learn Reactive Programming](http://reactive.how) - Cédric Soulas

* [Rx Visualization - Visualizes programming with RxJS](https://fingerpich.github.io/rx-visualization/) - Mojtaba Zarei

_RxJS 4에 관심이 있으십니까?_ [_Denis Stoyanov_](https://github.com/xgrommx) _의 훌륭한_ [_eBook_](https://xgrommx.github.io/rx-book/)_을 살펴보세요!_

## 번역

* [简体中文](https://rxjs-cn.github.io/learn-rxjs-operators)


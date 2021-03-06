# Car Racing Game

_By_ [_adamlubek_](https://github.com/adamlubek)

This recipe demonstrates RxJS implementation of Car Racing game.

## Example Code

\( [StackBlitz](https://stackblitz.com/edit/rxjs-car-racing?file=index.html) \)

![Car Racing](https://drive.google.com/uc?export=view&id=1geB1veKhXmqEeTqy5h23Lyo6dgsRRPjH)

### index.ts

```javascript
// RxJS v6+
import {
  interval,
  fromEvent,
  combineLatest,
  of,
  BehaviorSubject,
  noop
} from 'rxjs';
import {
  scan,
  tap,
  pluck,
  startWith,
  takeWhile,
  finalize,
  switchMap
} from 'rxjs/operators';
import { Car, Road, Player, Game } from './interfaces';
import { gameHeight, gameWidth, levelDuration } from './constants';
import { updateState } from './state';
import { render, renderGameOver } from './html-renderer';

const car = (x: number, y: number): Car => ({ x, y, scored: false });
const randomCar = (): Car =>
  car(0, Math.floor(Math.random() * Math.floor(gameWidth)));
const gameSpeed$ = new BehaviorSubject(200);

const road$ = gameSpeed$.pipe(
  switchMap(i =>
    interval(i).pipe(
      scan(
        (road: Road, _: number): Road => (
          (road.cars = road.cars.filter(c => c.x < gameHeight - 1)),
          road.cars[0].x === gameHeight / 2
            ? road.cars.push(randomCar())
            : noop,
          road.cars.forEach(c => c.x++),
          road
        ),
        { cars: [randomCar()] }
      )
    )
  )
);

const keys$ = fromEvent(document, 'keyup').pipe(
  startWith({ code: '' }),
  pluck('code')
);

const player$ = keys$.pipe(
  scan(
    (player: Player, key: string): Player => (
      (player.y +=
        key === 'ArrowLeft' && player.y > 0
          ? -1
          : key === 'ArrowRight' && player.y < gameWidth - 1
          ? 1
          : 0),
      player
    ),
    { y: 0 }
  )
);

const state$ = of({
  score: 1,
  lives: 3,
  level: 1,
  duration: levelDuration,
  interval: 200
});

const isNotGameOver = ([state]: Game) => state.lives > 0;

const game$ = combineLatest(state$, road$, player$).pipe(
  scan(updateState(gameSpeed$)),
  tap(render),
  takeWhile(isNotGameOver),
  finalize(renderGameOver)
);

game$.subscribe();
```

### state.ts

```javascript
import { BehaviorSubject, noop } from 'rxjs';
import { Game } from './interfaces';
import { gameHeight, gameWidth, levelDuration } from './constants';

const handleScoreIncrease = ([state, road, player]: Game) =>
  !road.cars[0].scored &&
  road.cars[0].y !== player.y &&
  road.cars[0].x === gameHeight - 1
    ? ((road.cars[0].scored = true), (state.score += 1))
    : noop;

const handleCollision = ([state, road, player]: Game) =>
  road.cars[0].x === gameHeight - 1 && road.cars[0].y === player.y
    ? (state.lives -= 1)
    : noop;

const updateSpeed = ([state]: Game, gameSpeed: BehaviorSubject<number>) => (
  (state.duration -= 10),
  state.duration < 0
    ? ((state.duration = levelDuration * state.level),
      state.level++,
      (state.interval -= state.interval > 60 ? 20 : 0),
      gameSpeed.next(state.interval))
    : () => {}
);

export const updateState = (gameSpeed: BehaviorSubject<number>) => (
  _,
  game: Game
) => (
  handleScoreIncrease(game),
  handleCollision(game),
  updateSpeed(game, gameSpeed),
  game
);
```

### html-renderer.ts

```javascript
import { Game } from './interfaces';
import { gameHeight, gameWidth, car, player } from './constants';

const createElem = (column: number) =>
  (elem => (
    (elem.style.display = 'inline-block'),
    (elem.style.marginLeft = '3px'),
    (elem.style.height = '12px'),
    (elem.style.width = '6px'),
    (elem.style.borderRadius = '40%'),
    (elem.style['background-color'] =
      column === car ? 'green' : column === player ? 'blue' : 'white'),
    elem
  ))(document.createElement('div'));

export const render = ([state, road, playerPosition]: Game) =>
  (renderFrame => (
    road.cars.forEach(c => (renderFrame[c.x][c.y] = car)),
    (document.getElementById(
      'game'
    ).innerHTML = `Score: ${state.score} Lives: ${state.lives} Level: ${state.level}`),
    (renderFrame[gameHeight - 1][playerPosition.y] = player),
    renderFrame.forEach(r => {
      const rowContainer = document.createElement('div');
      r.forEach(c => rowContainer.appendChild(createElem(c)));
      document.getElementById('game').appendChild(rowContainer);
    })
  ))(
    Array(gameHeight)
      .fill(0)
      .map(e => Array(gameWidth).fill(0))
  );

export const renderGameOver = () =>
  (document.getElementById('game').innerHTML += '<br/>GAME OVER!!!');
```

### interfaces.ts

```javascript
export interface Car {
  x: number;
  y: number;
  scored: boolean;
}

export interface Road {
  cars: Car[];
}

export interface State {
  score: number;
  lives: number;
  level: number;
  duration: number;
  interval: number;
}

export interface Player {
  y: number;
}

export type Game = [State, Road, Player];
```

### constants.ts

```javascript
export const gameHeight = 10;
export const gameWidth = 6;

export const levelDuration = 500;

export const car = 1;
export const player = 2;
```

## index.html

```markup
<style>
  .road {
    width: 100px;
    height: 180px;
    margin-top: 25px;
    overflow: hidden;
    position: absolute;
  }

  .dotted {
    margin-top: -100px;
    height: 300px;
    border-left: 2px dashed lightgray;
    position: absolute;
    animation: road-moving 1s infinite linear;
  }

  @keyframes road-moving {
    100% {
      transform: translateY(100px);
    }
  }
</style>

<div class="road">
  <div class="dotted" style="margin-left: 0px;"></div>
  <div class="dotted" style="margin-left: 9px;"></div>
  <div class="dotted" style="margin-left: 18px;"></div>
  <div class="dotted" style="margin-left: 27px;"></div>
  <div class="dotted" style="margin-left: 36px;"></div>
  <div class="dotted" style="margin-left: 45px;"></div>
  <div class="dotted" style="margin-left: 54px;"></div>
</div>
<div id="game"></div>
```

## Operators Used

* [BehaviorSubject](../subjects/behaviorsubject.md)
* [combineLatest](../recipes-1/combination/combinelatest.md)
* [finalize](../recipes-1/utility/finalize.md)
* [fromEvent](../recipes-1/creation/fromevent.md)
* [interval](../recipes-1/creation/interval.md)
* [of](../recipes-1/creation/of.md)
* [pluck](../recipes-1/transformation/pluck.md)
* [scan](../recipes-1/transformation/scan.md)
* [startWith](../recipes-1/combination/startwith.md)
* [switchMap](../recipes-1/transformation/switchmap.md)
* [takeWhile](../recipes-1/filtering/takewhile.md)
* [tap](../recipes-1/utility/do.md)


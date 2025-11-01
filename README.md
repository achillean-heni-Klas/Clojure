# Cospd Arena - Browser Battle Simulator

![JavaScript](https://img.shields.io/badge/javascript-vanilla-yellow)
![WebGL](https://img.shields.io/badge/webgl-2.0-orange)

**write bots in js, watch them fight in real-time**

## demo

[cospd-arena.io/play](https://cospd-arena.io/play)

## bot example

```javascript
// mybot.js
export function tick(me, enemies, arena) {
  const nearest = enemies.sort((a,b) => 
    distance(me, a) - distance(me, b)
  )[0]
  
  if (nearest && distance(me, nearest) < 100) {
    me.shoot(nearest.x, nearest.y)
  } else {
    me.moveTo(arena.width/2, arena.height/2)
  }
}
```

## run tournament

```bash
npx cospd-arena tournament \
  --bots bot1.js,bot2.js,bot3.js,bot4.js \
  --rounds 10 \
  --map desert
```

## game mechanics

- **health**: 100hp, regen 1hp/sec
- **energy**: attacks cost 10, regens 5/sec
- **vision**: 200px radius (fog of war)
- **speed**: 3px per tick

## maps

- desert (flat, no obstacles)
- maze (walls block bullets)
- islands (water = instant death)
- chaos (random obstacles spawn)

## leaderboard

top bots this week:

```
1. SnipeBot_v3    (47 wins)
2. DodgeMaster    (39 wins)
3. RandomWalker   (2 wins, somehow)
```

## implementation

uses **canvas-game-loop** ([canvas-game-loop.dev](https://canvas-game-loop.dev))

collision via **SAT.js** (separating axis theorem)

bots run in web workers (sandboxed)

## create account

```bash
cospd-arena register --username yourname
cospd-arena upload mybot.js
```

free tier: 100 matches/day

## known exploits (patched)

- ~~infinite loop freeze (v1.2)~~
- ~~memory leak via closure (v1.4)~~
- ~~teleport glitch (v1.7)~~
- coordinate overflow still works (shh)

inspired by screeps but simpler. no economy, no mining, just pure combat.

MIT • [github.com/battle-sim/cospd-arena](https://github.com/battle-sim/cospd-arena)


# PR Merge: 2025-11-01 07:58:27

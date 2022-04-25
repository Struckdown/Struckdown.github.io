---
layout: default
title: StarCraft2
permalink: /StarCraft2/
---

In Fall 2018, I took CMPUT 350: Advanced Games Programming which focuses on advanced AI in games and C++. In this class, our project for the last half of the course was to build a [StarCraft 2](https://starcraft2.com) bot from scratch and compete against the other teams. We formed into teams of 3-4 and went from there.

I had the pleasure of building our bot SegFault with:
* [Atharv Vohra](https://github.com/AtharvVohra)
* [Hugh Bagan](https://github.com/hughbagan)
* [Jolene Poulin](https://github.com/nienna73)

I personally am relatively familiar with StarCraft, having played it for over a decade and lead the discussion on game strategy. We didn't have a lot of time to make this bot, nor did we have any experience with making AI before this. As well, we all had other classes and responsibilities, meaning we had to pick a simple, robust strategy to work with if we wanted to do well.

We settled on a modification of a strategy I personally used when I played the game myself, 4-rax. Building an AI to be adaptable is tricky, since we're using hand-coded rules. As such, we wanted to build a wall to prevent early rushes from destroying us. We were given the map, so we hard-coded the location of the wall to save time, built 4 barracks, researched stim-packs, combat shields and +1 attack, and then rushed out with our army and workers, hoping to overwhelm the opposing bot before they could achieve whatever they were trying for. We also implemented some micro-management to focus fire on enemy units, stutter-step and use stimpack to try and get the most of our ranged units.

Our bot did fairly well as most other bots played towards the late game, trying to expand and play from there. We overall finished 2nd out of 10 bots which our team was surprised with but proud of.

![Building the Wall](/assets/buildingWall.gif)

In this following gif, you can really see SegFault microing all of the marines away from the enemy zealots simultaneously. The implementation was fairly naive - detect the closest hostile unit to a given marine, establish the direciton by subtracting one position from the other, and then move in that direction on a very short timer proportional to the marine's attack speed. If we were out of range, we would issue an attack order on that enemy unit instead, which would let the StarCraft 2 engine handle moving back towards the target. A weakness of this "move away" approach is that when cornered, if there's any geometry, there will be either an invalid command issued, or the marine will start to run past the hostile unit. Standing still is almost always worse, so running past the hostile unit, even for an attack or two is still better because we have changed the direction vector between the two units, and now should have new ground to run against. Lastely, we did not add stutter-stepping to the marauders, as we wanted them to serve as tanks to absorb the damage since they have a higher health pool and higher natural armor. In hindsight, I think we should have added stutter-stepping at a fraction, so they would still move away, but not as much (naturally putting them in the front).
![Sutterstep micro](/assets/stuttermicro.gif)

I have chosen to keep the Git Repository of the bot private at this time (to discourage other students from simply copying our work). If there is a desire to see it or discuss it, please contact me.
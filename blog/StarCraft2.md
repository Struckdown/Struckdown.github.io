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
![Sutterstep micro](/assets/stuttermicro.gif)


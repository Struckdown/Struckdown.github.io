---
layout: default
title: Light House
permalink: /LightHouse/
---

For Alberta Game Jam 2021, I put myself out there and teamed up randomly to make a game over the course of a weekend. I formed a team with three others (a programmer, a musician and an artist) I had never met before, and we spent the whole weekend putting together something we could be proud of. This is one of my favourite game jam outcomes so far, where we made a really tight and fun game, without overscoping while still getting in a reasonable amount of content and fun in.

For this project, I took on the parts of general team lead and general programming features. I created a Discord server for the four of us, as well as scheduling our regular meetings over the weekend and sparking the discussion using Google Jamboards. Myles, the other programmer worked on the core feature of laser reflections while I worked on everything else to create the framework for our game. This included me creating:
* Level selection
* The level start and finish conditions
* Designing about half of all the levels (including the notorious last level)
* Pickupable objects
* Screen transitions
* The powered states
* The rotating turrets
* Visual in-editor polish (eg, light effects, particle effects)
* Integrating all of the audio and art assets

Being highly familiar with Godot, none of these particular tasks were difficult or technically interesting, besides the lasers that I didn't work on. Though I did chat with the developer regarding their implementation to make sure I understood their work and thought it was quite clever. They used a linked list approach to create each laser fragment. We would test the object type we were hitting with a raycast and determine where the next laser should appear at, if anywhere. As each laser was updated, we could tell all the following lasers to update. I later enhanced the visuals by adding a particle effect, making it feel very pretty and alive. We didn't end up hiding the segment intersections using particles due to it being a game jam but that would be a good future improvement.


![LighthouseGameplay](/assets/LighthouseGameplay.png)

[Check out Light House on itch.io](https://dragonchasing.itch.io/light-house)

<iframe src="https://itch.io/embed/1159743" width="552" height="167" frameborder="0"><a href="https://dragonchasing.itch.io/light-house">Light House by Dragon Chasing Games, ElliotSnyder, Struckdown, wliamjackson</a></iframe>
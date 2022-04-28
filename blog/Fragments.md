---
layout: default
title: Fragments
permalink: /Fragments/
---

In Winter 2019, I took INT D 450: Computers and Games, which is the final course in the [Game Development Certificate](https://www.ualberta.ca/interdisciplinary-studies/computer-game-development) at the University of Alberta, which has us build a 30-minute game from start to finish using some game engine. Sounds a lot like CMPUT 250. Except, this time, we're not having our hands held. We chose the engine to work with, the platform to develop for, the target audience, the theme, the mood, the art direction, everything. Everything was made by us for this project.

The team:
Boris Fleysher - Producer, Programmer, Level Design
Stephen Melvin - Writer, Story Direction
Nate Spasiuk - Lead Designer, Artist, BGM
Andrew Somerville - Audio SFX, Programming support
Wang Dong - Programmer, Level Design
Guanfang Dong - Programmer, Level Design

As well, we had support from [Jeff Cho](jeffcho.com) and [Shelby Carleton](https://twitter.com/bdotexe?lang=en) as our Executive Producers, who mostly served as guidance and primary testers.

Our game was nomiated for "Best Game Development Practices", which we tied for first place with another team that was also incredible, [Ubiquitous Mayonnaise](https://itch.io/profile/ubiquitous-mayonnaise), who made Where The Flame Took You in that semester.
 
I personally worked on building many of the levels, protyping the crystal chasing mechanic, the monster's behaviour, implementing and integrating audio, animations and dialogue, and as the first person to go to when something goes wrong. I was responsible for ensuring a timly delivery of our project, including the weekly milestones and leading team meetings each week.

The pitch we settled on for this game was quite unusual and a bit of a hard sell. The idea that you are always being chased. Like, always always. Given our limited team size and skill sets, we needed to keep the scope small and simple. We decided on a top-down 2D game where we could use a 2D Nav-mesh to control the AI's pathing, and restrict the player to the same area as the AI typically. To manipulate the monster's movement, the player is able to stand in front of Crystals that emit light in particular directions. The way we handled this was extending a box collider that changed the monster's target from the player to the crystal. Once it's hitbox overlapped the crystals, the crystal would shatter, stop emitting light and the player would become the new target again. This lead to lots of cool little interactions where the monster would chase one crystal, and then start chasing another crystal once it overlapped the area of it. We actually really liked this behaviour, so we kept it in. We added dynamic lights to the game to help sell the shadow and light theme a bit more and improve the visual depth in the game. Fortunately for us, Godot already comes with a basic dynamic lights system that we were able to use without too much effort and it turned out pretty well!

![FragmentsTreasure.PNG](/assets/FragmentsChasingTheLight.PNG)
![FragmentsTreasure.PNG](/assets/FragmentsTreasure.PNG)

One little aspect I really liked about this game was that the story actually had two outcomes, depending on how many times you were ultimately caught by the AI! Unfortunately, we didn't get enough playtests in to determine what the right level of difficulty was, being a really time-pressure sensitive puzzle game likely means the difficulty was going to vary greatly for different players. I was in charge of most of the level design, so I tried really hard to clearly isolate mechanics in each individual level to teach them to the player, before later combining them in more and more complex levels. We ended up with 13 levels which wasn't too bad. While each level is just effectively a single room and can be played in under a minute, this was a necessary caveat of having a monster that always chases you and is likely to catch you. We didn't want the player to be frustrated by defeat, so we kept small bite-sized challenges in mind.

We were nearing the end of the semester and had to choose what to invest the remainder of our time in besides polish. We decided on one last small feature - level select, with a time attack component. With our design, it was relatively easy to add and low-risk, while being a nice little "extra" feature that I hadn't done before in any other games.

![FragmentsLevelSelect](/assets/FragmentsLevelSelect.PNG)

Play in browser and download the game at the following link!
[Windows and Mac Download Links](https://struckdown.itch.io/fragments)

<iframe src="https://itch.io/embed/406800" width="552" height="167" frameborder="0"><a href="https://struckdown.itch.io/fragments">Fragments by Struckdown</a></iframe>

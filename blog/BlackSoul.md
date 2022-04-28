---
layout: default
title: Black Soul
permalink: /BlackSoul/
---
# Black Soul

## Overview
In Summer 2018, my friend [Omer](https://github.com/omergosh) and myself were thinking about playing around in Unity to work on an RPG game idea we had, mostly to practice programming. We ended up accidentally stumbling across another one of our friend's, [Kieran](https://kierandowns.github.io) and he invited us to join him to make a game over the summer. And from there, we went on to make Black Soul.

Black Soul is a game made in [Godot 3](https://godotengine.org), built from the ground up. We started learning this engine, having never used it before and managed to make a top-down 2D action game in three months. We ended up learning a good lesson in scope and the difficulties of getting everything done in a timely fashion, especially since this was a passion hobby project and many of us were doing other things like working full or part time and had various other obligations.

## The Team:
* [Kieran Downs](https://kierandowns.github.io) (Executive Producer, Audio)
* [Boris Fleysher](https://struckdown.github.io) (Lead Developer, Lead Designer, Producer)
* Nelson Chen (Art, Sprites, Environment)
* [Taylor Folkersen](https://github.com/tfolkersen) (Programmer/Developer)
* [Omer Ahmed](https://github.com/Omergosh) (Programming Support)
* Jonas Liew (Story Direction)

I personally worked as the lead developer and designer for this project as well as taking on the role of the Producer to help hold meetings
and facilitate them when Kieran was unable to. The player movement, camera, turret behaviour, projectiles, level design, game flow and feel were all designed and made by me.

## Mechanics
Our core mechanic for this game, our razor if you will, was the idea of avoiding enemy projectiles and using them against their creators. Every mechanic, everything we designed always came back to this question. How can we tie in something to avoiding projectiles? 

### Player Powers
We added a dash mechanic to let you move through tight areas really quickly. I played around with the feel a bit, and I ended up deciding to let the player control the dash completely. My implementation can be summarized as increasing the player's movement speed, and then sharply decreasing it using an exponential decay, back to their original speed. Due to the large amount of focus on the character, we decided to visually indicate when the dash was available, but due to time constraints, we were forced to use tinting of the sprites instead of creating a new animation.

The next major mechanic we added was deflection. We gave the player the ability to reflect projectiles occasionally. This let the player access previously unavailable locations and solve new puzzle types, such as juggling a slow moving projectile across a room to open up a path. For this, we have an object that is offset from the player, but has the pivot attached to the player. We then rotate the pivot to always face the mouse, bringing the barrier with it. Like before, we didn't have an animation and instead tinted the player with a different color to indicate the cooldown.

![BlackSoulDeflection.png](/assets/BlackSoulDeflection.png)

And the last major power we added to the player was swapping. The summer was winding down and people were getting pretty tired to unfortunately we didn't have much time to polish this. This was implemented by performing a raytrace from the character's origin to the mouse's position in world space and checking against the first object hit with collision. On a successful match, we swapped the locations of the player and the hit object.

### Opposition
Throughout the experience, the player runs into enemy guards and turrets throughout the world. The turrets are invulnerable and require the player to duck, dodge, dip, dive, and dodge out of the way of their projectiles. We started with simple straightforward ones, that just move forward and later introduced more complex patterns and behaviours such as homing and angular homing projectiles that turned on a fixed timer a certain amount. I setup all of the work for the bullet emitters and their powerful pattern configuration to let the entire team design a room during one of our meetings. The final escape sequence was the result of Kieran's level prototype from that meeting! 

Each turret contains an emitter which creates a bullet object on a fixed timestep. I made the object into a template so that a turret could emit any time of bullet object, and then added a few parameters, such as allowing it to overwrite properties of the bullet if needed, such as creating slower bullets. I then allowed for multiple bullets to be emitted and the angle of seperation from them, allowing for spiral and flower like patterns to emerge. One of the later rooms has an absolute silly idea that one of our developers had - put turrets on a rotating object. So we put rotating objects on rotating objects and attached turrets to those. And it was a mess but made for a hilarious side room that we left in.

![BlackSoulTurretControls.PNG](/assets/BlackSoulTurretControls.PNG)

For the guard behaviour, I initially started the development on this though eventually one of the other developers took on it full time. The premise was simple - have two radi for the detection and undetection. You could lose detection by running away, but the undetection radius was larger. While you're in their undetection radius after having entered the detection radius, they enter their hostile state (using a state based machine) and start cycling between attacking and moving after you. I then added some doors that had a condition to wait for those guards to die, emitting a signal and letting the door know it could be closed. For saving progression between levels, we would write the guard's tree hierarchy plus the level name to disk in a dictionary stucture, ensuring we would always know the state of any given enemy at near instant speeds. Given the small scope of the game, the data size was not a concern.

### Some neat things about the game:
* There's a secret bonus room that can be reached through some backtracking when the swap ability is unlocked
* Three different bullet types with variable shotgun effects lead to some pretty cool flower patterns from turrets
* The camera shake was based on what I learned from a talk on "juice in games", using an exponential decay
* The deflection mechanic went through several iterations as we tried to figure out what felt the best for calcuating the reflection

Here's a screenshot in the early portion of the game where the player needs to weave between bullets and use them to break glass to open up additional paths.
![Screenshot of Black Soul Gameplay](/assets/BlackSoulGameplay.png)

## Conclusion
Given the fact that I learned an entire engine for this project and was working on it only on my downtime, I think it turned out pretty well. While no particular aspect of this game is incredibly complex, all these little things add up to make a pretty cool and complete game. It's really amazing what a game engine can do for you and the ways it can make your life easier. You don't need to create the universe from scratch to make an apple pie this way. While this project was complete enough, I think there's tons of room for polish and feel that could be put in. Unfortunately, as is with projects, like the summer, they too must end. It is dangerous to chase perfection as it can never be achieved and sometimes its just time to start a new project!

[Checkout the Github Repo here](https://github.com/TeamMaigo/BlackSoul)
[And the game here!](https://omergosh.itch.io/black-soul)

<iframe src="https://itch.io/embed/428833" width="552" height="167" frameborder="0"><a href="https://omergosh.itch.io/black-soul">Black Soul by Omergosh, Struckdown</a></iframe>
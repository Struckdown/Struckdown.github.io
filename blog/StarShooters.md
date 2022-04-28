---
layout: default
title: Star Shooters
permalink: /StarShooters/
---

In 2021, I decided to make a game in Godot. Singlehandedly. As much as I could do that is, without getting too much into making art and audio assets myself since that's not my skillset. And so I made an entire hour long experience using Godot 3 as a complete game.

![Star Shooters](/assets/StarShootersGameplay1.PNG)

There's a lot that went into this project. I worked on it a little bit each week for an entire year. I had the pitch for this game back in 2016, before I had even started university and before I had ever done any real programming or learned anything about it. So in 2021, I decided to start up this project because I knew I had the skills and the time to pull it off. The premise was simple. A top-down shoot-em up styled game, where the focus was all about grazing enemy projectiles to be able to fight back. You had to flirt with danger. One of the first things I got feedback on was that it was too tough. Like really hard. Which lead to the great suggestion someone gave - instead of instant death, you would lose some of your reserved energy instead of instantly dying. This tied into the core concept while still letting you have leeway to make some errors here and there if you played a bit safer.

## Bullet Emission
The core implementation for this game was the ability to generate bullet patterns. This game would live and die by the bullets and their patterns and making it sufficiently interesting. Like in [Black Soul](/BlackSoul), I needed to create a bullet emitter that I could freely reuse. On top of that, I needed to be able switch firing patterns for more advanced enemies. I broke this down into two separate classes. The BulletEmitter and the WeaponManager. The BulletEmitter was responsible strictly for emitting bullets and the WeaponManager controlled when the BulletEmitters were active.

However, there was another complication - I needed to be able to switch between multiple patterns, non-linearly. I wanted bosses to have multiple phases where each phase would have different patterns, but each phase would also have multiple patterns inside the phase itself. So a boss with 2 phases would have at least 4 different patterns (2 sets of 2 patterns). Switching between patterns during a phase was time based, while switching to the next set of patterns was health based. To do this, the WeaponManager class was defined recursively. Each BulletEmitter was added as a child of a WeaponManager, and would cycle between them on some time interval. However, a WeaponManager could have another WeaponManager as a child. The root WeaponManager would set which child WeaponManager was active, which then would recursively propogate down the chain, eventually ending with the leaf nodes which were always BulletEmitters.

In this following example, I get kinda creative with my usage of the heirarchy where I have BulletEmitters that are children of other BulletEmitters, which are just always active if their parent is active. They also inherit the rotation, which sometimes might be useful. In this case, one of the children is a "tracker" emitters, so it just always shoot towards the player's position, regardless of their rotation. In the other case, I use the rotation and offset it with another small rotation and a start offset to create a dual wave pattern. WeaponManager is the root here, and toggles between WeaponManager1 and WeaponManager2 based on health remaining. Which in this case is just simply 50%. Lastely, I had a BulletEmitter node off by itself, and that just creates an emitter that's always active, which I wanted for effect for this boss. 
![Boss Bullet Emitters Example](/assets/StarShooters/BossEmitterExample.PNG)

Dual Wave pattern snippet. The enemy is moving during this attack so it's kinda tough to see, but each wave is rotationally offset compared to the next.

![DualWave](/assets/StarShooters/DualWave.PNG)

I wanted *highly* customizable bullet properties for this game. I wanted to be able to control *everything*. The scale over time, the number of emissions, the speed, how many bullets were fired before it had to be reloaded, the angle of spread between bullets, how it calculated where the center bullet was, how long each bullet lived for, the spawn delay and so forth. I took a bit of inspiration from particle emitters with how much went into this class, but it only came out at \~440 lines of code, though it is still by far the largest single class in this entire project. And a bit of it, is just setting properties in the spawned bullet class.

![Bullet Emitters](/assets/StarShooters/BulletEmitterProperties.PNG)

## Target Prediction
One of the coolest little sub-problems I ended up solving for this problem was target prediction. I wanted enemies to be able to predict where you were moving and fire there instead, to give them a little tiny bit of "intelligence", even though I rarely used this special targeting style as it doesn't make much sense for any bullet that doesn't travel particularlly fast, and I tried to make bullets not too fast to make the game playable.

Given a player, moving in a straight line at constant speed towards some point and a hostile enemy, where should we try to hit the player as they are moving. We need to solve where to shoot, but to do that, we need to know when the collision would take place. We can model the problem as an expanding circle, representing anywhere the bullet could have reached after x time, and a line that is growing in some direction from a given point. Hmm, solving a circle line intersection problem? That sounds like quadratic time! We're looking to determine the roots of the equation, aka, where the line intersects the circle. It's possible the line only intersects the circle at negative values, meaning there are no solutions. It could also intersect the line twice at the same time, or in two seperate places.

![BulletDistanceGraph](/assets/StarShooters/BulletDistance.png)

The position of the bullet can be represented as:
`bulletPos(t) = originalPosition + time*bulletVelocity`
And the target's position is:
`targetPos(t) = targetOriginalPosition + time*targetVelocity`
We're looking for the values of t that satisfy this equation when they are set equal to one another. We don't know the velocity vector of the bullet at this time unfortunately. But we can still start solving here.
```
originalPosition + time*bulletVelocity = targetOriginalPosition + time*targetVelocity
orgPos + t*bulVel = tarOrgPos + t*tarVel
bulVel = (tarOrgPos + t*tarVel - orgPos) / t
bulVel = (tarOrgPos - orgPos) / t + tarVel
```
Since position is all relative, we can simplify a bit further and just say
`bulVel = (deltaPosition) / t + deltaVelocity`
We still don't know what bulVel is, but we do know that we want bulVel squared to be equal to speed squared (since the dot-product of a vector against itself equals the magnitude squared of that vector). So we can square both sides to remove the vector component and only worry about the scalar.
```
speed^2 = ( deltaPosition / t + deltaVelocity ) ^ 2
speed^2 = deltaVelocity^2 + 2(deltaPosition*deltaVelocity/t) + deltaPosition^2 / t^2
```
We can now finally adapt the quadratic equation to solve it from here as we now have a quadratic curve that can be represented as ax^2+bx+c. We substitute for each variable and we get:
* a = deltaVelocity ^ 2 - speed^2
* b = 2(deltaPosition\*deltaVelocity)
* c = deltaVelocity^2

https://www.gamedeveloper.com/programming/predictive-aim-mathematics-for-ai-targeting
https://stackoverflow.com/questions/2248876/2d-game-fire-at-a-moving-target-by-predicting-intersection-of-projectile-and-u

![quadraticFormula](/assets/StarShooters/quadraticFormula.jpg)



a = 
c = 

a = velocity of the projectile




## Particles
To add more flare to the game, it was necessary to have explosions. Some screen shaking of course, but more importantly, bits and pieces of debris needed to shoot out, and a series of explosions to hide the enemy disappearing. In particular, the explosions needed to be done in bulk. I needed to create a ton of animated sprites. Which didn't seem too bad until I ran the game in HTML and it seemed there was a stuttering issue whenever an enemy died. I figured it was likely related to the particles, so I decided to try object pooling, a game design practice for optimizing performance by pre-allocating all of the resources for something and then reusing them as needed instead of creating more. Instead of each enemy creating a particle system, they make a request to the Particle Manager, which then allocates the next available particle system. If none are available, the call simply fails. The particle manager keeps track of all the particle systems which are already loaded into memory using a circular array for each type of particle system. I only had a few that needed to be pooled, so this was fine for my scope. Unfortunately, this did not seem to fix the HTML stuttering issue and I didn't know how to properly debug it any further, so I was forced to write it off as HTML being unoptimized. Which I don't think surprises anyone.

![GemsAndExplosions](/assets/StarShooters/GemsAndExplosions.PNG)

In a similar style, another optimization I made was related to the gem spawning. Initially they had a hitch whenever a boss died because there were trying to spawn sometimes as many as 200 objects in a single frame. I instead spread out this work by limiting the amount of gems that could spawn per frame to around a dozen and then continuing to spawn until all gems had been spawned over many frames. Since this still all happened in just a dozen frames at most, the player could not see they weren't spawning all at once. Plus, there's a visual flare to having them spawn not all at once that is very much something I could have exacerbated for effect.


## Wave System
One of the other most important features for a top-down shooter game is that enemies have to come at you systematically in waves. I'd never written a wave manager before and this was something I was a bit iffy on how to do correctly. I decided that I wanted every level to be hand-crafted. I needed to be able to create a set of enemies for each wave, which each enemy was customized using the WeaponManagers and BulletEmitters mentioned earlier. Each enemy would have to start off-screen and then move somewhere onto the screen. I allowed each wave to have customized starting points, and then the target position was given either by raw coordinates as an offset, or a target position object. When the enemy spawned, it would drift towards the target position depending on which move pattern it was given. I then expanded this to allow for point path following. An enemy would move along a path until the end and then restart the path or despawn as appropriate. This allows for tons of variety in the enemy movements and when coupled with the enemy patterns, allows for a reasonably interesting game.

To manage this further, each wave had to have a specific advance condition. A wave would advance based on enemies in the wave slain, time or sometimes a custom parameter. This let some waves that would automatically self-destruct start the next wave before they were completely off screen, or allow a wave to spawn the next wave before the current wave was fully resolved to allow for mounting pressure. I then added a "checkpoint" wave that made sure all enemies were cleared out before advancing, as it was possible to advance to the boss with other enemies still around using this. This created a new conundrum though - enemies could be left on screen that were unkillable if they didn't create energy by grazing. I initially had prototyped all enemies to always give energy but found this created too much and was boring to play against because either you needed to graze hundreds of projectiles or grazing just a few gave you all the energy you needed. I added a new design constraint, that every enemy would always create energy or leave the screen and self-destruct.

By creating wave templates, all the wave manager needs to do is load and spawn each wave template for the given level, and once all waves have marked themselves as finished, the wave manager knows the level as a whole is finished. The waves are in charge of marking how they finish, and so dialogue in this game is actually also just another type of wave. Same with power-up waves. Even dialogue is just a wave with a custom finish signal relating to when the dialogue finishes.

![WaveManager](/assets/StarShooters/WaveManager.PNG)

## Shaders
Since I have worked in UE4 previously, I had done a bit of work with shaders and thought to use a few here and there for some effects. The player's shield is actually composed of a Perlin noise texture that wraps and pans slowly. I then create two circles, subtracting the smaller circle from the larger circle to create a donut. To give the donut a smooth fade in on the inside ring, we use the distance function as an input to a smooth step. We then multiply this donut shape against the alpha, creating a nice visual shield effect.

![DonutShaderOutline](/assets/StarShooters/DonutShader1.PNG)

![DonutShader](/assets/StarShooters/DonutShader.PNG)

The energy bar is also composed of a shader! It lerps from 0 to 1 on the v component of the uv map, transitioning from red to green. Like before, we have a hard cutoff of either the intended color or black using an IF statement, where the decision point is based on an input controlled by a script externally to match the player's energy percentage representation. Since the entire shader graph is very simple, I do not worry about the performance costs of using IF here. To add the white bar, I take the v axis, multiply it by two constants chosen arbitrarily based on the amount of percent the player loses in energy when they are hit, 1.25 and 1.3, and floor the results. Subtracting one from the other returns a thin band of white across a black background, that I can simply add into the final image.

## Conclusion
Phew, that's a lot of stuff! I haven't talked about the upgrade system, the stats tracking, the dialogue system or other things I'm not thinking of at the moment but they're all interesting in their own little ways. Instead of me talking more about this game, you should really play it and see for yourself! [Check it out here!](https://struckdown.itch.io/star-shooters)

<iframe src="https://itch.io/embed/1163830" width="552" height="167" frameborder="0"><a href="https://struckdown.itch.io/star-shooters">Star Shooters by Struckdown</a></iframe>



---
layout: default
title: Borbot
permalink: /Borbot/
---

In 2020, I decided to make a Discord bot using Python. One of the community servers I was on had just recently built one and I felt inspired to try to do something similar with my own takes on various things. A bunch of us were big into D&D at the time, so a dice roller was a simple example to recreate. And then I just kept adding features to it for fun because I knew you could do *anything* with Python and this was a really easy way to interface with the Discord API and make something kinda silly but fun!


The list of features:
* Dice roller
* Reaction roles
* Image with custom text that can be dynamically generated (basically the setup for meme formats)
* Cycling custom statuses (with limitations)
* Ask command for 8-ball answers
* Echo command (have the bot say something)
* Monitor command (no actual purpose)
* Simple character generator
* RPG system (with local data storage)
* Daily Quotes


## Dice Roller
The different features have different varying levels of complexity so I'll only explain a few of them in great detail.

The Dice roller takes in a string and attempts to clean it up, before parsing it, using the "d" character as the divider to create a partition. Tokens fall into a few categories.
* xdy, where x and y are some integer and d is a literal character
* Arithmetic operators (+,-)
* Integers (+4, -3)
From there, we convert all the xdys by generating a random number from 0 to y, x times. We can then sum them up and add all the integers in.

![DiceRoll](/assets/Borbot/DiceRoll.PNG)

## Reaction Roles, Custom Statuses, 8-Ball, Echo
Reaction roles was simply using the Discord API, nothing fancy there. Same with cycling custom statuses. Likewise, I added a generic 8-ball answering function for fun. You call the function and it returns one of the 8-ball replies completely at random. Echo was on the same calibur of just returning what you said in a given text channel and deleting your message (to give the implication the bot was speaking and sentient).
![RoleAssignment](/assets/Borbot/RoleAssignment.PNG)
![8Ball](/assets/Borbot/8Ball.PNG)
![BotSpeaks](/assets/Borbot/BotSpeaks.PNG)

## Text Overlay Over an Image Generation
The custom text image generation was me realizing you could build a discord bot and dynamically generate custom images, especially trivial if you were only adding text to an already existing image. I learned about the Pillow python module, played around with it a little bit and prototyped a very basic text overlay ontop of an already downloaded image to create the most basic format for a meme. I didn't bother working on it any further as it was mostly a proof of concept and I didn't really have anyone to share it with, but it had the potential to go further if there was any purpose or motivation to do so.

## Basic Procedural Character Generation
The character generation was made using a very simple procedural generation approach. Given a sentence format of A really liked B, we can randomly generate A and B from a list each respectively, and come up with unique sentences. James really liked apples. The Void Terror really liked the end of humanity. Two very different sentences, with the same root structure. I expanded this slightly to use a few different lists of words I had picked out with no interplay or restrictions between each choice, making each choice completely random and independant. 
![CharacterGeneration](/assets/Borbot/CharacterGeneration.PNG)

## RPG-esque Stats Tracking
Then, following this RPG trend, I decided to play around with a bit of local data storage. I started recording the amount of messages any given user had made while the bot was online, updating a value in a dictionary and saving the file locally as a JSON file. This could then be read whenever the bot was started up to resume the count and make for a fun little feature to see how often people were posting. Some further improvements would likely require more verbose data logging to allow for data analysis such as timestamps. We could then analyse when users would post and even graph it at that point.
![BorbotStats](/assets/Borbot/BorbotStats.PNG)

## Message of the Day
The next feature I wanted to add was the ability to generate a Message of the Day (MotD). This had been a popular feature historically with computers and it's something I've always enjoyed the concept of, x of the day, where something changes in an unknown way and you get a little something. With computers, getting something automatically once a day isn't too bad. What do I grab each day though? I wanted to do a quote of the day, so I needed to find a place that would have enough volatility that each day I could find a new quote reliably, without having to generate my own. So, using python's Beautiful Soup module, I was able to put together a very basic webscraper that would visit reddit.com/r/quotes and grab the top most quote of the day. The users there follow a very particular format, so parsing out the quote is relatively trivial and already done for me! Really simple implementation, very satisfying to get a new quote every day. And every once in a while, I see one that sticks with me for some time.

I love this one.
![BorbotQuote](/assets/Borbot/BorbotQuote.PNG)

## RPG Kit Expansion
And then I started brainstorming and talking too much about D&D and how I don't like the d20 system for player agency. So then I said, lets upgrade this bot to playtest some ideas. I started using this bot as a way to simulate drawing from a custom deck of cards and a bag of tokens.

The deck of cards were custom made objects with two parts, a title and description. We then create an array of these, shuffle it, and can treat it as a stack. As cards are drawn, we can put them in the discard stack which is another array. When we need to reshuffle, we can just append both arrays together as the new deck, shuffle and clear out the discard.

The bag of tokens works in a similar way, where it's an array composed of a series of Token objects that are composed of a name, effect and integer value, of which the name and effect may be null. Since the array is pretty small (<20 tokens typically), we can shuffle it before each draw without any concern for performance. We sample with replacement in this system, so we need not actually remove the token, and just peek at whatever is on the top after shuffling. If multiple tokens need to be drawn, we can just peek at the first n tokens, where is n is the number of tokens to draw. Shuold we need to remove a token from the bag, we can peek at the contents of the bag (which is just an array), and remove the nth index as needed. Likewise, we can always just append new tokens to the bag, since we shuffle before any draws.

![DeckOfCards](/assets/Borbot/DeckOfCards.PNG)
![ChaosBag](/assets/Borbot/ChaosBag.PNG)

## Conclusion
I had a lot of fun making this bot and it's been very handy for playtesting alternative D&D and TTRPG systems with the power of Python! There's a lot of great things you can do with the power of computers and this is a great just-for-fun example of a fun little hobby project.

[Check out the repository here!](https://github.com/Struckdown/BorBot)


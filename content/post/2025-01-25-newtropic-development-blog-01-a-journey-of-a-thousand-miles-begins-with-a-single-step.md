---
layout: blog
title: NewTropic Development Blog 01 - A journey of a thousand miles begins with
  a single step
description: This week has been a productive week. Let's talk about it.
date: 2025-01-25T13:13:00.000Z
image: https://i.imgur.com/csv66s9.png
categories:
  - This Week in NewTropica
tags:
  - Development News
  - Community News
---
# NEWTROPIC DEVELOPMENT BLOG #01

*Jan 24, 2025 - InitRanger, Programmer*

What's up, everyone? InitRanger here with the first of many blog posts about the development of NewTropic. Today I hope to give you some insights into what we have been working on the past week. I will go into detail about the following things:

- The game engine
- The movement system
- The ODIN framework
- Dialogue Nodes
- Public Roadmap
- Community

Here we go!

# THE GAME ENGINE

When the team was first formed, we discussed in length what tools we should use to develop the game. In the end, we settled on using the Godot game engine. We went over many options, and I want to go over those options with you today so you understand why we chose Godot.

Initially, there was talk about using bare C++ with something like SDL or GLFW. This idea was short-lived by the very fact that it would have increased development time hugely. The goal of this project is to make a game, not a game engine. We would have had to put a bunch of time into the development of the engine instead of the actual project. Given the nature of the game, it was doable but in the end, it was decided that our time was better spent using an existing engine instead of making our own.

Unreal Engine was briefly considered but was quickly ruled out due to it being completely overkill for a project like this. While 2D games are more than possible in Unreal Engine it's overkill to use the powerhouse that is Unreal for a 2D game like this. There was also the fact that our other programmer `Idiot` is more comfortable using raw code than the Unreal Engine blueprint scripting system. I rather not use Unreal Engine because there are additions that we would have to make to any engine and Unreal is not the most user-friendly when trying to add features to the engine itself.

***

![image](https://i.imgur.com/k9EoUYR.jpeg)

*Unreal Engines Blueprint Scripting*

***

The next engine we considered was Unity. Unity is a very strong engine for 2D games as well as indie games. The first reason we decided not to go with Unity is because of the Unity runtime situation that Unity announced in 2023. While Unity did ultimately back down on this after lots of public outcry, however they have lost all trust people had in them. There is no way to be sure they won't try something in the future and that is not a risk we wanted to take.

***

![image](https://i.imgur.com/o9L1VWB.jpeg)

*Unity Runtime Fee Chart*

***

There is also the fact of porting the game to consoles. The ultimate goal is to have NewTropic on as many platforms as possible including platforms like the Switch or PS5. This presents a problem if we choose to use Unity. Unity requires you to use Unity Pro if you want to port to console. This was a problem because Unity Pro would cost us **$2,200** a year. This would prevent us from porting for a long time if ever because nobody on the team can afford to do that year after year. The last smaller issue that we took issue with was the fact that source code access was locked behind their enterprise plan, and considering that we would want to make modifications to whatever engine we use to improve our workflow this was another nail in the coffin.

***

![image](https://i.imgur.com/9ac0hfI.png)

*Slightly out of date but still illustrates the point*

***

We then took a look at Game Maker 2. Game Maker 2 was a good-looking option and its pricing option for console exports was way more attractive compared to Unity. The biggest problem about Game Maker that we discovered was that it was not made for the style of game we wanted to make. Game Maker 2 was designed to make 2D-pixel art games and that is not the type of game we want to make. Technically Game Maker 2 can make other types of games, it can even make 3D games with enough work. The problem is that when you try and use an engine to make something it was not designed for you will eventually run into problems.

***

![image](https://i.imgur.com/MSF0LUW.png)

*Game Maker 2*

***

The last engine we took a look at was Godot. Right off the bat, the team liked the fact that Godot was open source. Godot also has the benefit of having a scripting language very similar to Python which also increases the potential number of people able to help on the project.

***

![image](https://i.imgur.com/3tv4dVe.jpeg)

*GDScript*

***

The biggest drawback to Godot is the lack of console support. This is due to the open-source nature of the engine, but since Godot is open source that means the team can add support for consoles to our fork of Godot. Godot is also future-proof due to having backing from companies such as Google, which paid a company to improve its Vulkan renderer.

Taking all of these facts into consideration we decided to use Godot. As the game is developed the team will continue to develop our framework and make modifications to the core engine.

Now that the boring stuff is out of the way let's actually talk about the progress that has been made this week.

***

# LET THERE BE MOVEMENT!
 
Our wonderful programmer `Idiot` has been hard at work on the games movement system. During the past week he has been working on replicating the original Poptropica's movement system and it's coming along very nicely.

***
[![Video about the movement system](https://img.youtube.com/vi/TVpmmenfXQU/0.jpg)](https://youtu.be/TVpmmenfXQU)

*It's a bit buggy and not pretty to look at but were proud of it so far*

***

There are still some bug to work out, UI and animations to be made but it's a really solid start.

Previously you have heard me talk about ODIN. You are probably wondering what that is.....

*right????*

# ODIN IS WITH US!

From the very start of the project, I knew we would need to make a framework that would not only make it easier to develop future islands and other content for the game but would also give the other programmers and designers access to advanced features without having to interact with complex code. That is where ODIN comes in.

ODIN (no fancy meaning yet...) is going to be a set of tools that both content creation easier and faster. ODIN will expose different APIs, such as the console APIs to the engine that way other developers don't have to work into complex C++ code and recompile the engine whenever they make changes. Outside of exposing APIs ODIN will have several native Godot tools to help out with development.

The first of these tools is called Dialogue Nodes. Dialogue Nodes is a node-based tool that will allow the team to make dialogue, missions, events, etc faster, due to the fact they won't manually have to touch any code.

Ok, that sounds cool and all but *what can ODIN CURRENTLY do????*

I'm so glad you asked.

# EXTRA! EXTRA! READ ALL ABOUT IT!

Currently the tool is in very early stages of development. It works by loading a GraphEdit node and from this node you can spawn custom GraphNodes. Currently there is only a comment node that will allow you to comment you graph.

***

![image](https://i.imgur.com/csv66s9.png)

*Current dialogue engine editor*

***

When saving nodes ODIN uses a custom save file format called `.ode` . The save file saves the data as JSON data so it can be easily read later when loading the file or when being read from an NPC. The contents of the save file look like this:

`[{"Position":"(920.0, 420.0)","Size":"(220.0, 300.0)","Type":"GraphNode","children":[{"Text":"Gravity Falls","Type":"TextEdit"}]},{"Position":"(1160.0, 420.0)","Size":"(340.0, 300.0)","Type":"GraphNode","children":[{"Text":"Start vs The Forces of Evil","Type":"TextEdit"}]},{"Position":"(920.0, 740.0)","Size":"(580.0, 220.0)","Type":"GraphNode","children":[{"Text":"Owl House","Type":"TextEdit"}]}]`

Doing it this way has many benefits. The first is that it takes up very little storage which keeps the final game size small, the next reason is because JSON is efficient and Godot has built-in support for reading and writing JSON data, and finally because JSON data can easily be encrypted. The files for this game will be encrypted but the dialogue engine will be made in such a way that the editor can be exported outside the game, meaning if we want to allow for user-created islands in the future then the community can use the tools we are developing now to create them.

More will be shown of the dialogue engine and other ODIN tools as they are further developed but for now here is a video of the current workflow:

***

[![Video about the Dialogue Engine](https://img.youtube.com/vi/dMPfXPf_-X0/0.jpg)](https://www.youtube.com/watch?v=dMPfXPf_-X0)

*The current dialogue engine workflow*

***

*All these updates are cool an all but what about the future?*

You sure ask a lot of questions but it just so happens I have an answer for that to.

# I'm the map! I'm the map!

The team wants this game to be a community orientated project, so decision was made to make a public Trello board where you can see what we are working on, our future goals, possible goals and even things that the you can vote on.

***

![image](https://i.imgur.com/btxTR0J.png)

*"He has such a way with words"*

***

There are a few small changes that will be made to the board in the coming days so give it time for everything to be sorted out but this should give the community a good idea on the current state of the project.

Speaking of the community...

# Invite your friends

As I have said before we want this project to be centered around the community. Invite your friends, talk with us in the server and have fun.

I know the server is not the best right now and I have some ideas that might make it more fun for everyone. Feel free to leave ideas in the Discord and if we think they are good then they just might make into the community voting phase and if they get enough votes then it will become a feature.

# Thank You!

Thank you all for being a part of the community and taking the time to read this blog post. Feel free to comment down below and let us know your thoughts. You guys are what make doing this project worth it. I know it didn't come out on Friday so hopefully it will be on time next week.

Until next time.....

InitRanger (Software Sorcerer)

---
title     : "#1 The game"
date      : "2026-03-13T12:00:00"
draft     : false
projects  : ["game-engine"]
---

For the last couple of weeks, I have been looking into working with OpenGL again. Previously, I have played around with OpenGL, physics engines such as Box2D, and entity component systems, and so on. However, I have never really properly tried to make anything except smaller demos. This time, I am trying to build something more substantial. More specifically, I want to make something I can call a "game".

After around 10,000 lines of code, I think I might have broken the initial barrier and now have something to work with. I am building most of the engine around EnTT, which is an entity component system (ECS) library for C++. I have also integrated Box2D nicely into the ECS system (for 2D physics), together with miniaudio for audio and music. I am trying to make as much of the codebase reusable as possible if I ever get tired of my current game idea, so I have made the following split:

- `core/`, where all game-agnostic, plumbing-like, and very domain-neutral code lives.
- `extensions/`, where still game-agnostic but more domain-focused code can be found.
- `game/`, where highly game-specific code lives, which I most likely will not be able to reuse in future projects.

I will add more posts here in the future, mainly to document my progress.

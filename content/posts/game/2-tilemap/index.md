---
title     : "#2 Tilemap"
date      : "2026-03-26T12:00:00"
draft     : false
projects  : ["game-engine"]
---

I am really fond of the game Deep Rock Galactic, especially the destructible terrain. In a past mini demo, I tried building something similar by creating so-called iso-surfaces using the marching squares algorithm. Initially, I was thinking about building something similar for my current game (but in 2D), but later decided to go for tilemaps instead.

The tilemap itself is an ECS entity. In my core layer, I added several tile-layer ECS components that can be attached to an entity in order to create these tilemaps. Right now, I have implemented the following layers:

- Visual "base" layer: Simple layer consisting of a grid mesh. The UV coordinates of the texture are baked into the vertices, allowing each tile to select a region from the texture atlas.
- Light layer: Consists of a single quad and a texture covering the entire tilemap. One texel is used per tile, which can individually be manipulated, thus creating quite interesting light effects.
- Collision layer: Layer containing handles into the physics engine, keeping track of collision shapes and bodies.

## The Light layer
The light layer I find particularly interesting, as I could quite easily implement Terraria-like lighting using different sampling settings.

{{< figure src="tilemap-gl_linear.png" width="100%" caption="Tilemap rendered using GL_NEAREST on the light texture. As can be seen, the light is quite rough, and one light texture texel (pixel) covers each tile in the visual layer." >}}

{{< figure src="tilemap-gl_nearest.png" width="100%" caption="Using the GL_LINEAR sampler setting, we are able to smooth the light a bit more." >}}

## The Collision layer

The collision layer is quite straightforward. It basically consists of a set of handles to Box2D shapes (and a rigid body). I know that I will use a lot of tiles in my game and did not want to create one shape per tile. Therefore, I created a box-merge algorithm that merges tile shapes so that fewer physical entities need to exist in the physics engine.

{{< figure src="tilemap-one-shape-per-tile.png" width="100%" caption="Example of a tilemap where each tile has its own physical shape." >}}

{{< figure src="tilemap-merged-shapes.png" width="100%" caption="Example of a tilemap after the box-merge algorithm has been implemented." >}}
---
layout: post
title:  "Whitelist RuleTile"
date:   2021-01-03 21:16:15 -0500
categories: Unity
---
If you've done a project using Tilemaps in Unity, you probably know about 2d-extras, the official Unity Github repo thats loaded with handy extensions to the base Tilemap kit.  One of the keey components of 2d-extras is the RuleTile - a Tile that will render a unique sprite depending on the neighbours of the tile.  This is extremely handy for 2D games, as it prevents a developer from having to write rules for tons of unique tiles (hence the name!). 

While my post on Autotiling covers the generation of these Ruletiles from editor script (to reduce how much repetitive work a developer has to do with the WYSIWYG editor), this post covers a solution to an obstacle most people hit right out the gate.

** Ruletiles are simply not smart enough **

most tiles you'll use (especially if you come from an RPG Maker workflow) Look something like this:

<img src="https://kpdwyer.github.io/assets/WhiteList/Clay.png" alt="Clay Autotile" style="zoom:200%;" /><img src="https://kpdwyer.github.io/assets/WhiteList/ShallowWater.png" alt="Shallow Water Autotile" style="zoom:200%;" />

These are very simple Autotiles - the clay tileset has shallow water at its edge, and the shallow water tileset has deep water at its edge. If we consider a case where these ruletiles are set up in the default manner, the boundary between these two tiles would appear as such:

![bad boundaries](/assets/WhiteList/clayandshallow.png)

This is because the RuleTile implementation has a very minimalist set of constraints: each Rule can check if a neighbour is The Same, Not The Same, or Don't Care.  In this case, we could layer multiple tilemaps and have each one support its own RuleTile, but in many cases thats not an ideal implementation.  The ideal Implementation is to add a tiny bit of complexity to the RuleTile, rather than a lot of complexity elsewhere.

Some solutions pointed online involve adding an enum to every tile to "group" tiles together.  So rather than the 3 basic constraint types (this, not this, and don't care),  Developers would implement their own groups, such as Caves, Sand, Grass, etc.  this is fine if all your tiles are using the same TileBase subclass, but often users need to mix and match basic tiles, RuleTiles, custom tiles, and more.  The grouping implementations I've seen involve every tile knowing its grouping (even if only a couple of RuleTiles actually *need* that information from the tile).

Rather, I chose to implement a simple WhitelistRuleTile.  This is a RuleTile with a `List<TileBase>` that a user can populate to adjust whether the Ruletile thinks a tile is in the "This" group or not.  Here's the output with our tiles from above:

![good boundaries](/assets/WhiteList/working.png)

As you can see, the shallow water tile no longer renders its edges against the clay boundary, allowing the art to work as its intended.  The bonus?  Since we use `TileBase` rather than any bespoke enums, we can use any type of Tile, and the Tile getting checked doesn't need any special logic at all - the data that drives the unique aspect of this tile remains local to this tile.

Enjoy!

<script src="https://gist.github.com/KPDwyer/2e6e36e3a256e5817cfaef6ad730851c.js"></script>

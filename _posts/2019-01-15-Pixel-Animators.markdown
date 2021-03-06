---
layout: post
title:  "Animators"
date:   2019-01-15 19:57:15 -0500
categories: Unity
---
I've been working through a couple of prototype ideas to get a feel for what might be my next big commute project.  Many of these ideas involve pixel art - something I used to practice a lot.  While I'm happy with beholdin', I feel as though I really failed to hit a low bar for visuals in the project, and I'd like to correct that.

While Unity has certainly built out some great 2D tools for pixel art (Pixel Perfect Camera, Tilemaps), I feel the pipeline for taking a series of frames and turning them into usable Animations leaves something to be desired.

I've started to work through this problem - So far, I'm generating Animation Clips from the project folder: with the included gist, simply select a group of sprites, right-click and select `Generate Animation.`  The ideal workflow involves generating an AnimatorController in some root folder, as well as clips in each sub folder based on alphanumerically sorted sprites.  I'll update as I go.

![My helpful screenshot](/assets/generateanimation.gif)

Note:  Lots of assumptions in this code - it isn't written as a catch-all solution, merely a solution to my struggles in this domain.  Lots of hardcoded values (samplerate is 12, everything loops, Animators are bound to a sprite named MainSprite, etc), but these are tweakable and should provide insight to those doing something similar.



<script src="https://gist.github.com/KPDwyer/136eed21b6c21bcda9436df2c4447a6d.js"></script>

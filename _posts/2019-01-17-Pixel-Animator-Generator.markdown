---
layout: post
title:  "Frame-based Animator Generator"
date:   2019-01-17 19:00:15 -0500
categories: Unity
---
I finished off writing a basic animation generator, given a very specific folder layout:

![File Structure](/assets/animgenerator_files.jpg)

This layout (and most of the code in this this gist) is simply set up the way that it is because it fits my current process.  None of this is meant to be universal or overly generic, but it's a good starting point if you're looking for something similar.

The tool can generate animator controllers + clips, or just clips from a folder or selection.

![Menu Hierarchy](/assets/animgenerator_menu.jpg)

I left in fairly basic `Debug.Log()` messages tracking (useful to track what has been done, rather than actual progress).

![Log Output](/assets/animgenerator_output.jpg)

And it does it's best to organize the resulting Animator Controller - in my game the art is along 4 cardinal directions, so it places the output in columns of 4 States for the sake of organization.

![Controller Output](/assets/animgenerator_controller.jpg)

Obviously there's still a lot of work involved (timing individual frames, setting up transitions + parameters, etc), but this saves some time - especially if the default method of dragging batches of sprites onto a animation clip doesn't quite cover your bases.


<script src="https://gist.github.com/KPDwyer/1c4a490e5d4e8eef7bbe0272126a2f20.js"></script>

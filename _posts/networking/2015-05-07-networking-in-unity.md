---
layout: post
category : networking
tagline: "keep it simple"
tags : [overview, beginner, unity, networking]
title : Networking Techniques in Unity
---
{% include JB/setup %}

* TOC
{:toc}

# Concepts Via Pictures

## Interpolation

## Extrapolation

## Events

# Implementations

## State Synchronisation (SS) vs Remote Procedure Call (RPC)

## Simple Interpolation and Extrapolation via RPC

# FAQ

## Should I use a networking framework/engine?

Depending on what you're doing, you may want to use a networking framework to help you along.
Sadly, pretty much all of these are game engine specific, so we'll only look at Unity specific technologies.
If you're looking to get something up quick and dirty that works well for simple networking tasks, try an engine!I've played with Photon and Bolt Engine for Unity, and in both cases the improvements were primarily ease of use.
I liked Bolt more than Photon because I felt its tutorials were supremely well done and the resulting code is a little cleaner.

If you're going to be doing anything more complex than basic character and level synchronisation, then avoid frameworks or be very careful when using them.
More complicated networking, particularly when the demand on number of objects to track increases, seems to still be best done by hand for your specific game.
But if you feel like you've reached this point, it might be a good time to ask yourself if you're overcomplicating matters.
I've tried a lot of different networking techniques and as a general rule the simplest approach tended to work almost as well as colossaly complicated approaches.

## Why is testing so hard? 

Unity doesn't have builtin testing for networked games.
This is a flaw on Unity's part, you're not going crazy.
Unreal Engine does have some networking testing that can be run from the editor.

Best thing to do seems to be to set up a script to run some $n$ copies of your game.
But if you're going to be maintaining networking in those copies, you need to actually make physical copies of the game on your disc.
So a script to run your games might look something like:

```
for value in range n
  copy gamename.exe gamename-n.exe
  copy gamecontentfolder gamecontentfolder-n
  gamename.exe --client
gamename.exe --host
```

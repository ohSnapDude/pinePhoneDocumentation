# Hitting your head on a rock

In other words, stuff I do while trying to compile stuff but wound up being unnecessary. This file is basically a behind-the-scenes of my thought process; I'm not perfect XP

You get to see what I *try* to do but they either don't work, or they work and I didn't have to do it.

## General

### always get a <packageName>-dev first

I have a bad habbit of getting something like ffmpeg for example and then getting ffmpeg-dev. You just need to get the -dev as it almost always grabs the other binary for you as well.

## Docker

I got exposure to Docker during an internship a while back. It was awesome and quickly got addicted to it. After that though, I didn't have any uses for it anymore, that is until the miraculous pinephone came in to existance. And by that I mean random dependency errors that I was getting on said pinephone. In general it was a good time to brush up, needed to badly so this was a good excuse!

## qTox

### compiling libvpx

This is a component in qTox that google has some involvement in. They wrote this as a way to work with video encoding, which qTox uses to stream your webcam or desktop.

...I didn't need to go this route, I thought I did because it wasn't being found through `apk search`, *however* that ripples down to another problem. In my docker instance I accidentally deleted every other repo besides edge/testing. You can see where that went; I didn't see the package therefore I thought it didn't exist (oops). Moral of the story, when appending to a new file, use this `>>` instead of `>` this in your shell, it will save you 30 minutes of your phone getting hot just to compile something that's already there XP

In the event you *do* need to compile this, I can help you though because the source code doesn't compile on it's own. Rather it freaks out because `diff` from busybox is different from the one from `diffutils` (doesn't exist on alpine) in that there is no `--version` command. Simply skipping that check lets you compile, it's dumb but otherwise interesting.
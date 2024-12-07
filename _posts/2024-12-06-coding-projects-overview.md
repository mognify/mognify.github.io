---
layout: post
title: Coding Projects Overview
date: 2024-12-06 13:49 -0600
description: Nothing
categories: [General, Software]
tags: [tool, video, software]
pin: true
---

- [Movie Dialogue Removal]({% post_url 2024-12-06-dialogue-removal %})
- Mass download all personal instagram reels

<h1> General thoughts:</h1>
__The computer should help focus you__

```text
people are right to rice up their linux Uis.
The OS UI should be
dopamine-spikingly pleasant when you're doing something productive.
The computer should give you
a dopamine kick when it believes you're performing productively.
This can be based off user-defined goals
``` 

---

## Orient ML Selfbot
```text
Make the computer imitate you
by constantly being fed your input
and identifying triggers and triggered behavioral patterns
It uses this to predict your next action
then suggests and offers to perform
```
- Written in python with a focus on OS independence
- Constant engine: record input, structure in json file for that hour, every hour the ML is fed the last hour's input record json file... the ML is 
- First phase: prediction
	- based on the predicted next action steps
	- the program will highlight areas where it thinks you'll click (with transparent Qt frameless panes)
	- it will transparently overlay the text of what it thinks you'll next (frameless 90% transparent pane with text) where it thinks you'll type
- Second phase: performance
	- everything in the first phase except it offers to click/type where it predicts it needs to based on what it sees
- Third phase: autonomous
	- it can be trusted to be productive if left alone

---

## Sublime plugin
- Sublime .md post expansion plugin:
	- When it identifies a referenced post, e.g. ``- [Movie Dialogue Removal]({% post_url 2024-12-06-dialogue-removal %})``
		- then it checks if that post actually exists. If it doesn't, then it generates it with the default values, titled after its file name.
	- Keyboard control groups with different programs instead of restricted to just the same program type
		- Windows key + 1 should minimize all other applications and bring up a set of windows, all laid out a certain way
		- pre-specified window dimensions, 
---
layout: post
title: Coding Projects Overview
date: 2024-12-06 13:49 -0600
description: Nothing
categories: [General, Software]
tags: [tool, video, software]
pin: true
---

<h1>This site</h1>
Tags = "Home"
Home = "Feed"

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

---

## Custom Windows File Explorer
- File system contents fed into GUI that displays them according to jekyll/.md formatting

## Command Generator
- "When I say 'I like this', do the following"
	- then perform a series of clicks/keystrokes (pc/phone)

## Playlist creator
- Get all the videos in a directory
	- Play them one at a time
	- For each video, if i say "yes", add it to the playlist
	- If i say "no", skip it and dont play it in this session again

## Browser Redirect Rule
- Twitter main page should redirect to your profile
- Instagram main page should redirect to your profile

## Clipboard Sidepane GUI
- on clipboard change, if it contains text:
	- create text file with the contents of the updated clipboard
- another script watches for new text files in that folder
	- when it detects one, then it updates the GUI sidepane with it
	- you can right-click on these items and if it's e.g. a youtube, instagram, tiktok link then there's a download option

## Instagram Reel Download -> Reel Movie
Another instagram account of mine that I can send reels to and have it download onto my PC
So I'm not spamming Borpi with them from my phone
For my desktop: just go through my clipboard history and queue up downloading all instagram reels found
They become a video at the end of the month that i can then share with her

## LLM-generated commit description

## LLM-generated blog tags
- the state of the post (public/hidden)
- the topic of the post (identifying topics of discussion)


## Markdown-enabled Obsidian notes (notes in general)

## Streamlined way to add/modify posts

## OCR MTG card price checker
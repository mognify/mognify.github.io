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
- ~~Tags = "Home"~~
- ~~Home = "Feed"~~

- "Hidden" category pages won't show up on website
	- unless the user authenticates into vps


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

## Android clipboard auto-export to PC

## Computer usage reminder
- every 20 minutes:
	- Windows + D is pressed by bot
	- A voice tells you to get up and look around; enjoy the scenery
		- And the voice says an excerpt from a useful book related to your overall goals, but unrelated to the current task at hand

## Android clipboard export to PC

## Discord bot channel
- Whenever an instagram/youtube/twitter link is posted:
	- If the post has an image/video, then extract that and repost it in a separate read-only channel
	- Then delete the image if an image/video was found

## Discord server JSON export
- Every moon cycle, export as much information about the content in a channel as possible into a JSON file
	- Then clear the channel and post the JSON file in another read-only channel

## Local Voice Synthesis
- Feed it mp3 voice recordings of me monologuing

## Discord Gallery Bot
- v1
python discord bot code example:
1. The bot will be invited to a guild by a user
2. The bot will have access to see all the messages and delete all the messages and create a new channel

the bot will have a slash command (/repost)
where the command is posted in a specific channel

what the command does is:
within the channel where the command was run:
parse all the messages in the channel and extract the text of each post into a json file on the local machine
when it's finished parsing through all the messages in the channel, then it uploads the json file to the channel

it needs to retain the 

- v2
python discord bot code example:
it will have all Intents

on initialization:
- for each server the bot is in:
	- it checks if a channel exists named "atrium"... if it doesn't exist, create it
	- if can't create it and it doesnt exist, then skip the guild for everything else further during this session

whenever a user sends a message that contains a youtube, instagram, twitter, or tiktok link:
	- download the video/images from that link and repost them in "atrium" channel
	- also create a thread on that triggering message and repost the image/video contents there as well

whenever a user sends a message that contains a video/image:
	- repost that image/video in "atrium" channel

if the bot crashes, it needs to automatically restart

all the downloaded media will be stored locally in this folder: 
- F:\downloads_by_month\2024-12
	- "2024-12" only applied if it was downloaded in december 2024
	- If it's e.g. January 2025, then the contents would be saved in F:\downloads_by_month\2025-01

## Discord targetted channel instagram link media extraction
python discord bot code example:
prereq: the bot will have all intents
when the bot is DM'd, check if the message they were sent contains a channel ID (e.g. "990039368376934461")
if it does, then check all the guilds the bot is in for a channel with ID

if there is a guild like that, then check all the messages in that channel
for each message that does not contain a thread, but does contain an instagram link:
create a thread, and download the video/images from that instagram link and write "saved" in the thread. Store them locally at this file directory as well: "F:\downloads_by_month\MMMM-DD" where MMMM-DD is e.g. 2024-12 since this is december 2024, but next month is jan 2025 so the folder name then would be 2024-01
also maintain a local sqlite database of all the messages found and whether or not they had a thread and if they had an instagram link (of course once a thread is created then it's marked true, as in it did have a thread)
i also need it so that if the bot encounters any errors, especially in downloading the media, then it will make a note of that and be able to return to that particular instagram download later... if it encounters an instagram error like this then it should wait a while before trying again, so as not to overload the instagram API. It should go from most recent message to least recent of course
the name of the downloaded folder should contain as much information about the video source as possible, specifically: the username of the instagram account that posted the video and the date the video was uploaded, as well as the url ID of the video maybe (the first two are mandatory, this third one is optional)... this information and more should also be stored in the sqlite database related to this video information

## Astronomical Object Colongitude-Based Schedule/Alarms
- Track the colongitude of the sun and moon
- e.g. when the sun is between -10 and 5 degrees colongitude, then it's the sunrise that must be viewed
- When the moon is between 6 and 15, then it's the moon's gold/silver transition that must be viewed
## Astronomical Horizon-ALtitude-Based Triggers
python code example:
tells me, based on my location (first-time running i need to enter my location either by street address or by coordinates, and then in the future it recalls what i put down (auto-fills the text field with previous input) and allows me to update it each time i run it)

the end-goal of this is to have it tell me, based on my location, what time the sun or moon will be at certain degree altitudes
so like i want to know when the moon will be between 5 and 15 degrees altitude (i want to be able to make it run a command prompt command when this occurs, whether it just rose to 5 degrees altitude or if it set to 15 degrees altitude
and for the sun i want to know when the sun enters -10 degrees altitude while rising or enters 5 degrees altitude while setting
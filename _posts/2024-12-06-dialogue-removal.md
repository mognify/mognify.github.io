---
layout: post
title: Mp4 Dialogue Removal
date: 2024-12-06 07:13 -0600
description: Nothing
categories: [Software, Tools]
tags: [tool, video, software]
pin: true
---
```
i want a python script that i can feed an mp4 movie into and have it cut out any parts with detected dialogue

so basically it would need to identify where speech is recognized, timestamp it, and feed it into an mp4 cutter
```

The purpose for this is because some movies have cringe dialogue but great non-dialogue parts, and other videos have great dialogue but cringe non-dialogue parts.

Can also be applied to mp3s maybe, and with video monologues. Or maybe you just want to get a clip out of a video.

GPT prompt:
I want a series of scripts, and they must be independent of the internet, i.e. they must run locally and offline. Here's how many parts (individual scripts) it will have:
1. Feed mp4 into script, and script outputs the timestamp ranges (json) of where speech is recognized, including what was said
2. Feed mp4 into script and timestamp ranges (json) and separate the video into 2 folders of the included clips and excluded clips
3. Compile multiple mp4 files into a single mp4 file (gluing multiple videos together)

### Code for 1: extract-speech-timestamps.py

Prerequisite: [Vosk model downloaded](<https://alphacephei.com/vosk/models>)
```python
import json
import os
import subprocess
from vosk import Model, KaldiRecognizer

def extract_speech_timestamps(mp4_file, model_path="vosk-model"):
    audio_file = "temp_audio.wav"
    timestamps_json = "dialogue_timestamps.json"

    # Extract audio from video
    subprocess.run(["ffmpeg", "-i", mp4_file, "-ar", "16000", "-ac", "1", audio_file, "-y"])
    
    # Load Vosk model and process audio
    model = Model(model_path)
    recognizer = KaldiRecognizer(model, 16000)

    with open(audio_file, "rb") as f:
        data = f.read()
        recognizer.AcceptWaveform(data)
        results = json.loads(recognizer.FinalResult())

    # Extract timestamps and save to JSON
    speech_segments = []
    for word in results.get("result", []):
        speech_segments.append({
            "start": word["start"],
            "end": word["end"]
        })
    with open(timestamps_json, "w") as f:
        json.dump(speech_segments, f, indent=4)

    os.remove(audio_file)
    return timestamps_json
```

### Code for 2: split-vid-by-timestamps.py
```python
import os
import json
import subprocess

def split_video_non_dialogue(mp4_file, timestamps_json, output_folder):
    with open(timestamps_json, "r") as f:
        timestamps = json.load(f)

    os.makedirs(output_folder, exist_ok=True)

    # Determine non-dialogue ranges
    video_duration = float(subprocess.check_output(
        ["ffprobe", "-v", "error", "-show_entries", "format=duration",
         "-of", "default=noprint_wrappers=1:nokey=1", mp4_file]).decode().strip())

    non_dialogue_ranges = []
    previous_end = 0.0
    for segment in timestamps:
        start = segment["start"]
        if start > previous_end:
            non_dialogue_ranges.append({"start": previous_end, "end": start})
        previous_end = segment["end"]
    if previous_end < video_duration:
        non_dialogue_ranges.append({"start": previous_end, "end": video_duration})

    # Split video into non-dialogue clips
    non_dialogue_clips = []
    for idx, segment in enumerate(non_dialogue_ranges):
        clip_file = os.path.join(output_folder, f"non_dialogue_clip_{idx+1}.mp4")
        start, end = segment["start"], segment["end"]
        subprocess.run(["ffmpeg", "-i", mp4_file, "-ss", str(start), "-to", str(end),
                        "-c", "copy", clip_file, "-y"])
        non_dialogue_clips.append(clip_file)

    return non_dialogue_clips
```

### Code for 3: combine-multiple-mp4s.py
```python
import os
import subprocess

def concatenate_videos(mp4_files, output_file):
    # Create a temporary file list for FFmpeg
    with open("file_list.txt", "w") as f:
        for file in mp4_files:
            f.write(f"file '{file}'\n")

    subprocess.run(["ffmpeg", "-f", "concat", "-safe", "0", "-i", "file_list.txt",
                    "-c", "copy", output_file, "-y"])
    os.remove("file_list.txt")
```

### Master script (calls the others): remove-dialogue.py
```python
from scripts.extract_speech_timestamps import extract_speech_timestamps
from scripts.split_video import split_video_non_dialogue
from scripts.concatenate_videos import concatenate_videos
import os

def remove_dialogue_and_combine(mp4_file, model_path="vosk-model", output_file="output_non_dialogue.mp4"):
    print("Step 1: Extracting speech timestamps...")
    timestamps_json = extract_speech_timestamps(mp4_file, model_path)

    print("Step 2: Splitting video into non-dialogue sections...")
    non_dialogue_folder = "non_dialogue_clips"
    non_dialogue_clips = split_video_non_dialogue(mp4_file, timestamps_json, non_dialogue_folder)

    print("Step 3: Combining non-dialogue clips into a single video...")
    concatenate_videos(non_dialogue_clips, output_file)

    print(f"Final video without dialogue saved to {output_file}")

# Example Usage
if __name__ == "__main__":
    input_video = "input.mp4"  # Replace with your input video file
    remove_dialogue_and_combine(input_video)
```

Example result:
{% include embed/youtube.html id='qqeRfleqiYc' %}
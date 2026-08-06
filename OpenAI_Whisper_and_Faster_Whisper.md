# OpenAI Whisper and Faster-Whisper

## What is OpenAI Whisper?

OpenAI Whisper is an Automatic Speech Recognition (ASR) model that
converts speech into text.

### Common Uses

-   Voice assistants
-   Meeting transcription
-   Podcast subtitles
-   Video captions
-   Voice input for AI chatbots

------------------------------------------------------------------------

## What is Faster-Whisper?

Faster-Whisper is an optimized implementation of Whisper built on
**CTranslate2**.

### Advantages

-   Faster inference
-   Lower memory usage
-   Better CPU performance
-   GPU acceleration
-   Production-friendly

------------------------------------------------------------------------

## Whisper vs Faster-Whisper

  Feature           Whisper    Faster-Whisper
  ----------------- ---------- ----------------
  Speed             Moderate   Faster
  Memory            Higher     Lower
  CPU Performance   Good       Excellent
  GPU Support       Yes        Optimized

------------------------------------------------------------------------

## Installation

### Install Faster-Whisper

``` bash
pip install faster-whisper
```

### Install FFmpeg

Verify installation:

``` bash
ffmpeg -version
```

------------------------------------------------------------------------

## Basic Example

``` python
from faster_whisper import WhisperModel

model = WhisperModel("base")

segments, info = model.transcribe("sample.wav")

for segment in segments:
    print(segment.text)
```

------------------------------------------------------------------------

## Available Models

-   tiny
-   base
-   small
-   medium
-   large-v3

------------------------------------------------------------------------

## Useful Parameters

``` python
segments, info = model.transcribe(
    "sample.wav",
    beam_size=5,
    language="en"
)
```

------------------------------------------------------------------------

## Supported Formats

-   WAV
-   MP3
-   FLAC
-   M4A
-   OGG
-   MP4

------------------------------------------------------------------------

## Save Output

``` python
text = ""

for segment in segments:
    text += segment.text + " "

with open("output.txt", "w", encoding="utf-8") as f:
    f.write(text)
```

------------------------------------------------------------------------

## AI Workflow

User Speaks → Faster-Whisper → Speech to Text → LLM → AI Response

------------------------------------------------------------------------

## Key Takeaways

-   Whisper converts speech into text.
-   Faster-Whisper is a faster implementation based on CTranslate2.
-   Install using `pip install faster-whisper`.
-   FFmpeg is required for most audio formats.
-   Faster-Whisper is ideal for AI assistants and voice-enabled RAG
    applications.

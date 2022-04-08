---
description: Audio format conversion
---

# FFmpeg

{% embed url="https://linuxconfig.org/ffmpeg-audio-format-conversions" %}

### Audio conversion examples

Check out some of the audio conversion examples below to see how ffmpeg can convert your files to different formats. We’ve compiled some of the most common options here. Note that ffmpeg has many additional quality settings and other options. It’s recommended to check out the man page and include the necessary flags in your commands.

### WAV – Waveform Audio File Format

###

#### wav to mp3

Convert wav to mp3 with ffmpeg:

***

***

```
$ ffmpeg -i audio.wav -acodec libmp3lame audio.mp3
```

#### wav to ogg

Convert wav to ogg with ffmpeg:

```
$ ffmpeg -i audio.wav -acodec libvorbis audio.ogg
```

#### wav to aac

Convert wav to acc with ffmpeg:

```
$ ffmpeg -i audio.wav  -acodec libfaac audio.aac
```

#### wav to ac3

Convert wav to ac3 with ffmpeg:

```
$ ffmpeg -i audio.wav -acodec ac3 audio.mp3
```

### OGG – Free, open standard container

#### ogg to mp3

Convert ogg to mp3 with ffmpeg:

```
$ ffmpeg -i audio.ogg -acodec libmp3lame audio.mp3
```

#### ogg to wav

Convert ogg to wav with ffmpeg:

```
$ ffmpeg -i audio.ogg audio.wav
```

#### ogg to aac

Convert ogg to aac with ffmpeg:

```
$ ffmpeg -i audio.ogg  -acodec libfaac audio.aac
```

#### ogg to ac3

Convert ogg to ac3 with ffmpeg:

```
$ ffmpeg -i audio.ogg -acodec ac3 audio.ac3
```

### AC3 – Acoustic Coder 3

***

***

#### ac3 to mp3

Convert ac3 to mp3 with ffmpeg:

```
$ ffmpeg -i audio.ac3 -acodec libmp3lame audio.mp3
```

#### ac3 to wav

Convert ac3 to wav with ffmpeg:

```
$ ffmpeg -i audio.ac3 audio.wav
```

#### ac3 to aac

Convert ac3 to aac with ffmpeg:

```
$ ffmpeg -i audio.ac3 -acodec libfaac audio.aac
```

#### ac3 to ogg

Convert ac3 to ogg with ffmpeg:

```
$ ffmpeg -i audio.ac3 -acodec libvorbis audio.ogg
```

### AAC – Advanced Audio Coding

#### aac to mp3

Convert aac to mp3 with ffmpeg:

```
$ ffmpeg -i audio.aac -acodec libmp3lame audio.mp3
```

#### aac to wav

Convert aac to wav with ffmpeg:

```
$ ffmpeg -i audio.aac audio.wav
```

#### aac to ac3

Convert aac to ac3 with ffmpeg:

```
$ ffmpeg -i audio.aac -acodec ac3 audio.ac3
```

#### aac to ogg

Convert aac to ogg with ffmpeg:

```
$ ffmpeg -i audio.aac -libvorbis audio.ogg
```

***

***

### Closing Thoughts

In this guide, we saw how to install the ffmpeg suite on major Linux distros, then use the `ffmpeg` command to convert audio files between different formats. Our examples contained some of the most common formats, but many more exist, and the ffmpeg software is packed with options. You can adapt our examples to your own needs, while customizing your commands with further options found in the ffmpeg man pages.

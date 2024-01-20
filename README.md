# Video Editing

# Table of Contents
 - [About](#about)
 - [Trim](#trim)
 - [Speed Up and Slow Down](#speed-up-and-slow-down)
 - [Format Conversion](#format-conversion)
 - [Convert from Portrait to Landscape](#convert-from-portrait-to-landscape)
 
# About 

This is a small tutorial to edit videos using Linux.

# Trim 

```bash
ffmpeg -i <PATH_TO_VIDEO> -ss 00:03 -to 01:07 -c:v libx264 -crf 30 <NEW_VIDEO_NAME>
```
**<em>NOTE: </em>** This will trim the video from 3s to 1m07s, making a total video length of 1m04s.

# Speed Up and Slow Down

```bash
ffmpeg -i <PATH_TO_VIDEO> -vf  "setpts=0.25*PTS" <NEW_VIDEO_NAME>
```
**<em>NOTE: </em>** This will speed up by 4 the video (1/0.25 = 4).

```bash
ffmpeg -i <PATH_TO_VIDEO> -vf  "setpts=4*PTS" <NEW_VIDEO_NAME>
```
**<em>NOTE: </em>** This will slown down the video by 4 the video.

# Format Conversion

**<em>NOTE: </em>** This will convert a video format to another one. 

```bash
ffmpeg -i <FORMAT1> <FORMAT2>
```

For example:

```bash
ffmpeg -i video.mkv converted_video.gif
```


# Convert from Portrait to Landscape

```bash
ffmpeg -i <PATH_TO_VIDEO> -vf "scale=1280:720:force_original_aspect_ratio=decrease,pad=1280:720:-1:-1:color=black" <NEW_VIDEO_NAME>
```
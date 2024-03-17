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

**IMPORTANT:** Sometimes the quality of the converted video can be bad. For exmple large pixels can be seen in GIFs, it's likely due to the limited color palette and resolution of GIF images. Here are a few additional tips you can try to mitigate this issue:

* **Reduce the color depth**: GIFs typically use a limited color palette (often 256 colors), which can lead to pixelation, especially in videos with gradients or smooth color transitions. You can try reducing the color depth to improve quality. For example:
    ```bash
    ffmpeg -i input.mkv -vf "scale=320:-1:flags=lanczos,split[s0][s1];[s0]palettegen[p];[s1][p]paletteuse" output.gif
    ```
    This command reduces the color depth while applying the Lanczos scaling algorithm for better quality.

* **Increase the output resolution**: While this may increase file size, it can also help mitigate pixelation issues, especially if the original video has a higher resolution. Try increasing the output resolution while keeping the aspect ratio intact. For example:
    ```bash
    ffmpeg -i input.mkv -vf "scale=640:-1:flags=lanczos,split[s0][s1];[s0]palettegen[p];[s1][p]paletteuse" output.gif
    ```
    This scales the output GIF to 640 pixels wide while maintaining the aspect ratio.

* **Try different scaling algorithms**: Different scaling algorithms may produce different results in terms of pixelation. Experiment with different algorithms such as lanczos, bicubic, or nearest_neighbor to see which one works best for your video. For example:
    ```bash
    ffmpeg -i input.mkv -vf "scale=320:-1:flags=neighbor,split[s0][s1];[s0]palettegen[p];[s1][p]paletteuse" output.gif
    ```
    This command uses the **nearest_neighbor** scaling algorithm.

* **Adjust dithering options**: Dithering can help reduce pixelation by simulating additional colors and smoothing out transitions between them. You can experiment with different dithering options to see if it improves the quality of your GIF. For example:
    ```bash
    ffmpeg -i input.mkv -vf "scale=320:-1:flags=lanczos,split[s0][s1];[s0]palettegen[p];[s1][p]paletteuse=dither=bayer:bayer_scale=5" output.gif
    ```
    This command applies Bayer dithering with a scale factor of 5.

**Experiment with these options to find the combination that produces the best results for your specific video. Keep in mind that there may be trade-offs between quality and file size.**
# Convert from Portrait to Landscape

```bash
ffmpeg -i <PATH_TO_VIDEO> -vf "scale=1280:720:force_original_aspect_ratio=decrease,pad=1280:720:-1:-1:color=black" <NEW_VIDEO_NAME>
```
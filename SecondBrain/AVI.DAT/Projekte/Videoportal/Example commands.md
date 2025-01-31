https://videoportal.mcs-thueringen.de/system/files/videos/50949c95-5983-4bf3-9449-fd8221220ba3/original.mp4


## Transcode to 720p

```bash
ffmpeg -i /daten/home/developer/working_folder/drupal/files_private/videos/50949c95-5983-4bf3-9449-fd8221220ba3/original.mp4 -y -movflags +faststart -vf scale=1280:720 -c:a aac -b:a 96k -c:v h264_nvenc -profile:v main -qmin 31 -qmax 36 -preset slow -bf 2 -g 125 -i_qfactor 1.1 -b_qfactor 1.25 -pix_fmt yuv420p 720p.mp4
```

## Scene detection

```bash
ffmpeg -i /daten/home/developer/working_folder/drupal/files_private\videos/b328b03d-1a21-432c-a4b5-70e78df84c81/original.mp4 -y -an -filter:v select='gt(scene,0.4)',showinfo -f null NUL
```
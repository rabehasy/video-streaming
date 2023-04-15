 
 Générer des fichiers HLS (HTTP Live Streaming) à partir d'une source vidéo en utilisant FFmpeg

```
ffmpeg -i ./sources/video.mp4 \
    -vf scale=-1:720 \
    -c:v libx264 \
    -b:v 2M \
    -g 60 \
    -keyint_min 60 \
    -sc_threshold 0 \
    -c:a aac \
    -b:a 128k \
    -hls_time 6 \
    -hls_playlist_type vod \
    -hls_segment_filename "./hls-generated/video_720p_%03d.ts" \
    ./hls-generated/video_720p.m3u8
```

Create file **./hls-generated/main.m3u8** and put this content

```
#EXTM3U
#EXT-X-VERSION:3
#EXT-X-STREAM-INF:BANDWIDTH=2100000,RESOLUTION=1280x720
video_720p.m3u8
```

Générer un fichier DASH (Dynamic Adaptive Streaming over HTTP) à partir d'une source vidéo en utilisant FFmpeg.

```
ffmpeg -i ./sources/video.mp4 \
    -map 0:v:0 -map 0:a:0 \
    -c:v libx264 \
    -b:v 1M \
    -c:a aac \
    -b:a 128k \
    -f dash \
    -use_timeline 1 -use_template 1 \
    -adaptation_sets "id=0,streams=v id=1,streams=a" \
    -seg_duration 5 \
    -streaming 1 \
    ./ffmpeg-dash-generated/manifest.mpd
```

**-i ./sources/video.mp4**: spécifie le fichier d'entrée.

**-map 0:v:0 -map 0:a:0**: sélectionne les flux vidéo et audio de la source.

**-c:v libx264**: spécifie le codec vidéo à utiliser, dans ce cas, libx264.

**-b:v 1M**: définit le débit binaire (bitrate) de la vidéo à 1 Mbps.

**-c:a aac**: spécifie le codec audio à utiliser, dans ce cas, aac.

**-b:a 128k**: définit le débit binaire (bitrate) de l'audio à 128 kbps.

**-f dash**: spécifie le format de sortie, dans ce cas, DASH.

**-use_timeline 1 -use_template 1**: active l'utilisation de la chronologie et du modèle dans le fichier MPD (Media Presentation Description).

**-adaptation_sets "id=0,streams=v id=1,streams=a"**: définit les ensembles d'adaptation pour les flux vidéo et audio.

**-seg_duration 5**: définit la durée de chaque segment à 5 secondes.

**-streaming 1**: active le mode de streaming pour générer un MPD en direct.

**./ffmpeg-dash-generated/manifest.mpd**: spécifie le fichier de sortie
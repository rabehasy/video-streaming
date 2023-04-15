Run this command from root project

```
ffmpeg \
    -re -i ./sources/video.mp4 \
    -c:v libx264 \
    -preset veryfast \
    -maxrate 2500k \
    -bufsize 5000k \
    -g 50 \
    -c:a aac \
    -b:a 160k \
    -ac 2 \
    -ar 44100 \
    -f flv \
    -b:v 2000k \
    -vf "scale=1280:720" \
    -flvflags no_duration_filesize \
    rtmp://127.0.0.1/live/stream
```

**-re** : Lire la vidéo à la vitesse normale (simuler le flux en direct).

**-i input.mp4** : Spécifiez le fichier d'entrée (votre vidéo préenregistrée).

**-c:v libx264** : Utilisez le codec vidéo H.264.

**-preset veryfast** : Utilisez un préréglage d'encodage pour équilibrer la qualité et la vitesse de l'encodage.

**-maxrate 2500k** : Limitez le débit binaire vidéo à 2500 kbps.

**-bufsize 5000k** : Définissez la taille du tampon pour le débit binaire vidéo.

**-g 50** : Configurez un intervalle de 50 images entre les images clés (keyframes).

**-c:a aac** : Utilisez le codec audio AAC.

**-b:a 160k** : Configurez un débit binaire audio de 160 kbps.

**-ac 2** : Utilisez 2 canaux audio (stéréo).

**-ar 44100** : Configurez une fréquence d'échantillonnage audio de 44100 Hz.

**-f flv** : Utilisez le format FLV pour le flux en direct.

Run this command from root project

```
ffmpeg \
    -i rtmp://127.0.0.1/live/stream \
    -codec:v libx264 \
    -codec:a aac \
    -strict -2 \
    -f hls \
    -hls_time 6 \
    -hls_list_size 10 \
    -hls_wrap 10 \
    ./live/live.m3u8
```



When "**live**" ends 

```
rm -f ./live/*
```
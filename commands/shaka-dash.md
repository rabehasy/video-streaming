# Installation de Shaka-packager

Avec docker

```
docker pull google/shaka-packager
```

Lancer le container 

```
docker run -v ./:/media -it --rm google/shaka-packager
```

Une fois à l'intérieur du container, lancer la commande pour générer un manifest MPD

```
packager \
    input=./sources/video.mp4,stream=audio,output=./shaka-dash-generated/audio.m4a \
    input=./source/video.mp4,stream=video,output=./shaka-dash-generated/video.m4v \
    --mpd_output ./shaka-dash-generated/manifest.mpd
```

Cette commande génère des segments audio et vidéo ainsi qu'un fichier de manifeste DASH (manifest.mpd).

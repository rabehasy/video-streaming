# Installation de Nginx et rtmp module

```
sudo apt update
sudo apt install nginx 
sudo apt install libnginx-mod-rtmp
```

# Configuration

Modifier la configuration

```
sudo nano /etc/nginx/nginx.conf
```

Et ajouter

```
rtmp {
    server {
        listen 1935;
        chunk_size 4096;
        allow publish 127.0.0.1;
        deny publish all;

        application live {
                live on;
                record off;
        }
    }
}
```

Recharger le service **Nginx**

```
sudo systemctl reload nginx.service
```
# Création des DNS

```
sudo vim /etc/hosts
```

Et ajouter la ligne suivante

```
127.0.0.1   hls.localhost live-testing-streaming.localhost
```

# Création du fichier de .conf  pour hls.localhost

```
cd /etc/nginx/sites-available
sudo touch hls.conf
sudo vim hls.conf
```

Et ajouter le contenu suivant

```
server {
    listen 81;
    listen [::]:81;

    server_name hls.localhost;

    location / {
            return 404;
    }

    location /hls/ {
        alias /var/html/;
        types {
            application/vnd.apple.mpegurl m3u8;
            video/mp2t ts;
        }
        add_header Cache-Control no-cache;
        add_header Access-Control-Allow-Origin *;
    }
}
```

# Création du fichier de .conf  pour hls.localhost

```
cd /etc/nginx/sites-available
sudo touch live-testing-streaming.conf
sudo vim live-testing-streaming.conf
```

```
server {
	listen 81;
	listen [::]:81;

	server_name live-testing-streaming.localhost;
	root /var/html/websites;
	index index.html;

	location / {
        try_files $uri $uri/ =404;
    }
}
```

Tester la bonne configuration

```
sudo nginx -t
```

Si pas d'erreur, redémarrer **nginx**

```
sudo systemctl restart nginx
```

# Tester

Aller à l'URL : http://live-testing-streaming.localhost:81/
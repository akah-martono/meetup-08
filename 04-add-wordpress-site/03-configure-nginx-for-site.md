# Configure SSL & nginx for Site

## Get SSL certificate
Sebelum request certificate pastikan A record pada domain sudah diarahkan ke IP VPS
Buat sertifikat let's encrypt:
```bash
sudo certbot --nginx certonly -d mitra.web.id -d www.mitra.web.id
```


## Add nginx config for site
Buat konfigurasi nginx untuk website yang ingin dibuat:
```bash
sudo nano /etc/nginx/sites-available/mitra.web.id
```

Isi dengan konfigurasi berikut:
```ssh_config
server {
    listen 443 ssl;
    listen [::]:443 ssl;
    http2 on;

    server_name www.mitra.web.id;

    ssl_certificate /etc/letsencrypt/live/mitra.web.id/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/mitra.web.id/privkey.pem;

    access_log /home/mitra/mitra.web.id/logs/access.log;
    error_log /home/mitra/mitra.web.id/logs/error.log;

    root /home/mitra/mitra.web.id/public/;
    index index.php;

    location ~ \.php$ {
        try_files $uri =404;
        fastcgi_split_path_info ^(.+\.php)(/.+)$;
        fastcgi_pass unix:/run/php/php-mitra.sock;
        fastcgi_index index.php;
        include fastcgi.conf;
    }
}

server {
    listen 443 ssl;
    listen [::]:443 ssl;
    http2 on;

    server_name mitra.web.id;

    ssl_certificate /etc/letsencrypt/live/mitra.web.id/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/mitra.web.id/privkey.pem;

    return 301 https://www.mitra.web.id$request_uri;
}

server {
    listen 80;
    listen [::]:80;

    server_name mitra.web.id www.mitra.web.id;

    return 301 https://www.mitra.web.id$request_uri;
}
```


Buat symlink ke sites-enabled
```bash
sudo ln -s /etc/nginx/sites-available/mitra.web.id /etc/nginx/sites-enabled/mitra.web.id
```

## Restart nginx
Periksa apakah konfigurasi yang kita ubah aman:
```bash
sudo nginx -t
```
Jika aman, restart:
```bash
sudo service nginx restart
```
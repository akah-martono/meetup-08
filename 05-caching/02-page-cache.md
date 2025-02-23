# Page Cache

## Install WP Super Cache


## Cnnfigure nginx for WP Super Cache
Buat folder inc di /etc/nginx:
```bash
sudo mkdir /etc/nginx/inc
```

Buat konfigurasi menggunakan nano
```bash
sudo nano /etc/nginx/inc/wsc.conf
```

Include file wsc.conf pada konfigurasi web
```bash
sudo nano /etc/nginx/sites-available/mitra.web.id
```

Ganti bagian block "location / {" dengan:
```text
include /etc/nginx/inc/wsc.conf;
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
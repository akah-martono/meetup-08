# Install and Configure NGINX 

## Install nginx
Gunakan repo nginx dari Ondřej Surý:
```bash
sudo add-apt-repository ppa:ondrej/nginx -y
sudo apt update
```

Install nginx:
```bash
sudo apt install nginx -y
```
Konfirmasi bahwa nginx telah terinstal:
```bash
nginx -v
```

## Configure nginx
Docs: 
- https://nginx.org/en/docs/http/ngx_http_core_module.html

Periksa CPU pada server (perhatikan jumlah corenya):
```bash
lscpu
```

Melihat batas jumlah file yang dapat dibuka / open file limit:
```bash
ulimit -n
```

Buka nginx.conf:
```bash
sudo nano /etc/nginx/nginx.conf
```

### main Context
Sesuaikan worker_processes (maksimal sejumlah CPU core):
```ssh_config
user www-data; 
worker_processes 1;
pid /run/nginx.pid; 
error_log /var/log/nginx/error.log; 
include /etc/nginx/modules-enabled/*.conf;
```

### events Context
Sesuaikan worker_connections (sejumlah open file limit) dan aktifkan multi_accept agar dapat menerima beberapa koneksi sekaligus:
```ssh_config
worker_connections 1024;
multi_accept on;
```

### http Context
#### Basic Settings
Default keepalive_timeout terlalu lama untuk WordPress yaitu 75s, set keepalive_timeout 15s:
```ssh_config
keepalive_timeout 15s;
```

Optimizing Performance for Serving Content
Docs: https://docs.nginx.com/nginx/admin-guide/web-server/serving-static-content/#optimizing-performance-for-serving-content
Set sendfile dan tcp_nopush on:
```ssh_config
sendfile on;
tcp_nopush on;
```

Set types_hash_max_size dan client_max_body_size: 
```ssh_config
types_hash_max_size 2048;    
client_max_body_size 64m;
```

Agar tidak menampilkan informasi tentang nginx di response header, set server_tokens off: 
```ssh_config
server_tokens off;
```

#### SSL Settings
Biarkan apa adanya
```ssh_config
ssl_protocols TLSv1 TLSv1.1 TLSv1.2 TLSv1.3; # Dropping SSLv3, ref: POODLE
ssl_prefer_server_ciphers on;
```

#### Logging Settings
Biarkan apa adanya
```ssh_config
access_log /var/log/nginx/access.log;
```

#### Gzip Settings
Docs: https://nginx.org/en/docs/http/ngx_http_gzip_module.html
```ssh_config
gzip on;
gzip_vary on;
gzip_proxied any;
gzip_comp_level 6;
gzip_types text/plain text/css application/json application/javascript text/xml application/xml application/xml+rss text/javascript;
```

#### Virtual Host Configs
Biarkan apa adanya
```ssh_config
include /etc/nginx/conf.d/*.conf;
include /etc/nginx/sites-enabled/*;
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

## Hasil Perubahan
Berikut isi nginx.conf setelah perubahan yang kita lakukan:
```ssh_conf
user www-data;
worker_processes 1;
pid /run/nginx.pid;
error_log /var/log/nginx/error.log;
include /etc/nginx/modules-enabled/*.conf;

events {
        worker_connections 1024;
        multi_accept on;
}

http {

    ##
    # Basic Settings
    ##

    keepalive_timeout 15;
    sendfile on;
    tcp_nopush on;
    types_hash_max_size 2048;    
    client_max_body_size 64m;
    server_tokens off;

    include /etc/nginx/mime.types;
    default_type application/octet-stream;

    ##
    # SSL Settings
    ##

    ssl_protocols TLSv1 TLSv1.1 TLSv1.2 TLSv1.3; # Dropping SSLv3, ref: POODLE
    ssl_prefer_server_ciphers on;

    ##
    # Logging Settings
    ##

    access_log /var/log/nginx/access.log;

    ##
    # Gzip Settings
    ##

    gzip on;
    gzip_vary on;
    gzip_proxied any;
    gzip_comp_level 6;
    gzip_types text/plain text/css application/json application/javascript text/xml application/xml application/xml+rss text/javascript;

    ##
    # Virtual Host Configs
    ##

    include /etc/nginx/conf.d/*.conf;
    include /etc/nginx/sites-enabled/*;
}
```
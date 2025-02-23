# Install PHP

## Install PHP 8.3
Gunakan repo PHP 8.3 dari Ondřej Surý:
```bash
sudo add-apt-repository ppa:ondrej/php -y
sudo apt update
```

Install PHP 8.3 beserta paket-paket yang dibutuhkan beserta:
```bash
sudo apt install php8.3-fpm php8.3-common php8.3-mysql \
php8.3-xml php8.3-intl php8.3-curl php8.3-gd \
php8.3-imagick php8.3-cli php8.3-dev php8.3-imap \
php8.3-mbstring php8.3-opcache php8.3-redis \
php8.3-soap php8.3-zip -y
```

Konfirmasi bahwa PHP 8.3 telah terinstal:
```bash
php-fpm8.3 -v
```


# Install WP CLI

## Download wp-cli.phar
Docs: https://make.wordpress.org/cli/handbook/guides/installing/

Download wp-cli.phar menggunakan curl:
```bash
curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar
```

Periksa apakah bisa jalan:
```bash
php wp-cli.phar --info
```

Jadikan executable dan pindahkan ke PATH (bin) agar bisa dijalankan dari mana saja:
```bash
chmod +x wp-cli.phar
sudo mv wp-cli.phar /usr/local/bin/wp
```

Test hasilnya:
```bash
wp --info
```
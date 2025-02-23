# Install WordPress Menggunakan WP-CLI

## Ganti user dan pindah ke folder WordPress
Ganti user dengan pemilik website
```bash
sudo su mitra
```

Pindah ke folder website yang telah dibuat sebelumnya
```bash
cd /home/mitra/mitra.web.id/public
```


## Download WordPress
Download WordPress terbaru
```bash
wp core download
```

Download WordPress terbaru
```bash
wp core config --dbname=mitra_db --dbuser=mitra_user --dbpass='Workshop@WPBogor2025'
```

Install WordPress
```bash
wp core install --skip-email --url=https://www.mitra.web.id --title='Workshop WPBogor' --admin_user=akah --admin_email=akah@wpbogor.org --admin_password='password'
```

Uninstall Plugin dan Theme yang tidak diperlukan
```bash
wp plugin delete akismet
wp plugin delete hello
wp theme delete twentytwentyfour
wp theme delete twentytwentythree
```
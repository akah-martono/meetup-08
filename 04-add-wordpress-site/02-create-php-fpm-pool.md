# Create PHP-FPM Pool

Jika masih ada default pool, dihapus/rename saja
```bash
sudo mv /etc/php/8.3/fpm/pool.d/www.conf /etc/php/8.3/fpm/pool.d/www.conf.bak
```

## Create PHP-FPM Pool Config
Buat file PHP-FPM pool menggunakan nano
```bash
sudo nano /etc/php/8.3/fpm/pool.d/mitra.conf
```

Isi dengan config berikut:
```ssh_conf
[mitra]
user = mitra
group = mitra

listen = /run/php/php-mitra.sock

listen.owner = www-data
listen.group = www-data

pm = dynamic
pm.max_children = 5
pm.start_servers = 2
pm.min_spare_servers = 1
pm.max_spare_servers = 3

php_admin_value[memory_limit] = 256M
php_admin_value[upload_max_filesize] = 64M
php_admin_value[post_max_size] = 64M
php_admin_value[opcache.enable_file_override] = 1
php_admin_value[disable_functions] = exec,passthru,shell_exec,system
```

Simpan dengan Ctrl+O lalu keluar editor dengan Ctrl+X

## Restart PHP-FPM
Periksa apakah konfigurasi yang kita ubah aman:
```bash
sudo php-fpm8.3 -t
```
Jika aman, restart:
```bash
sudo service php8.3-fpm restart
```
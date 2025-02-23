# Create User and Folder

## Create User
Buat user untuk website yang ingin kita buat
```bash
sudo useradd mitra
```

Masukkan user tersebut ke group www-data
```bash
sudo usermod -a -G mitra www-data
```

## Create Folder
Buat folder untuk website yang ingin kita buat
```bash
sudo mkdir -p /home/mitra/domain.com/public
sudo mkdir -p /home/mitra/domain.com/logs
```

Jadikan user yang kita buat sebelumnya sebegai pemilik folder
```bash
sudo chown -R mitra:mitra /home/mitra
```

Ganti _mitra_ dengan user yang ingin dibuat
Ganti _domain.com_ dengan domai yang ingin digunakan

## Buat PHP-FPM Pool

Jika masih ada default pool, dihapus/rename saja
```bash
sudo mv /etc/php/8.3/fpm/pool.d/www.conf /etc/php/8.3/fpm/pool.d/www.conf.bak
```

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
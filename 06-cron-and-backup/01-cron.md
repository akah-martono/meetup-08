# Configure CRON

## Ganti user dan pindah ke folder WordPress
Ganti user dengan pemilik website
```bash
sudo su mitra
```

Set CRON
```bash
crontab -e
```
Pilih 1. /bin/nano

Isi dengan knfigurasi berikut
```ssh_config
*/5 * * * * cd /home/mitra/mitra.web.id/public; /usr/local/bin/wp cron event run --due-now >/dev/null 2>&1
```

Pindah ke folder website yang telah dibuat sebelumnya
```bash
cd /home/mitra/mitra.web.id/public
```

Disable WordPress CRON menggunakan WP-CLI
```bash
wp config set DISABLE_WP_CRON true --raw
```


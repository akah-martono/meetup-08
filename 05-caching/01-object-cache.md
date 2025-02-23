# Install Object Cache

## Install Redis
Tambah repo dari Redis:
```bash
curl -fsSL https://packages.redis.io/gpg | sudo gpg --dearmor -o /usr/share/keyrings/redis-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/redis-archive-keyring.gpg] https://packages.redis.io/deb $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/redis.list
sudo apt update
```

Install Redis dan Restart PHP
```bash
sudo apt install redis-server -y
sudo service php8.3-fpm restart
```

Pastikan Redis tetap jalan meskipun server direboot
```bash
sudo systemctl enable redis-server
```

## Install Plugin Redis Object Cache by Till Krüss
Install Plugin Redis Object Cache dari: https://wordpress.org/plugins/redis-cache/
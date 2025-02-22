# Configure Uncomplicated Firewall

## Install ufw
Menginstall Uncomplicated Firewall
```bash
sudo apt install ufw
```

## Allow the ports for SSH (22), HTTP (80), and HTTPS (443)
Mengijinkan port 22 (SSH), 80 (HTTP), dan 443 (HTTPS)
```bash
sudo ufw allow ssh
sudo ufw allow http
sudo ufw allow https
```

## Review rules
Review rules yang telah dibuat
```bash
sudo ufw show added
```

## Enable rules
Mengaktifkan rules yang telah dibuat
```bash
sudo ufw enable
```

## Confirm that the new rules are active
Memastikan rules aktif
```bash
sudo ufw status verbose
```

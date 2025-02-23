# Create Database for Site

## Access MariaDB
Log in to the MariaDB database server.
```bash
sudo mariadb -u root -p
```
masukkan password yang sudah dibuat sebelumnya


Create database:
```sql
CREATE DATABASE mitra_db CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_520_ci;
```

Create user:
```sql
CREATE USER 'mitra_user'@'localhost' IDENTIFIED BY 'Workshop@WPBogor2025';
```

Grant privilege:
```sql
GRANT ALL PRIVILEGES ON mitra_db.* TO 'mitra_user'@'localhost';
```

FLush/refresh privileges:
```sql
FLUSH PRIVILEGES;
```

Keluar dari MariaDB
```sql
exit;
```
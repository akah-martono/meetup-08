# Login & Setup Timezone

## Login

Login dengan SSH Key:
```bash
ssh -i ~/.ssh/wpbogor.pem wpbogor@103.175.218.112
```

Login tanpa SSH Key:
```bash
ssh wpbogor@103.175.218.112
```
Ganti _wpbogor.pem_ dengan file SSH key  
Ganti _wpbogor_ dengan user  
Ganti _103.175.218.112_ dengan IP VPS  

## Setup Timezone
Menyesuaikan waktu server dengan timezone kita:
```bash
sudo dpkg-reconfigure tzdata
```


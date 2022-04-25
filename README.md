# Jetson Nano

## Set up steps

## Set Up Swap File
ตรวจดูขนาดของ Swap File ด้วยคำสั่ง 
```
free -m
```

ยกเลิก nvzramconfig ด้วยคำสั่ง
```
sudo systemctl disable nvzramconfig
```

สร้าง Swap File ขนาด 4GB เพื่อให้ระบบมีประสิทธิภาพที่ดีด้วยคำสั่ง
```
sudo fallocate -l 4G /mnt/4GB.swap
sudo chmod 600 /mnt/4GB.swap
sudo mkswap /mnt/4GB.swap
sudo nano /etc/fstab
```

ในไฟล์ fstab เติมข้อมูลบรรทัดต่อไปนี้
```
/dev/root   /   ext4    defaults    0   1
/mnt/4GB.swap   swap    swap    defaults 0 0
```

แล้วรีบูตเครื่อง จากนั้นสามารถตรวจสอบขนาดของ Swap File อีกครั้ง
```
free -m
```
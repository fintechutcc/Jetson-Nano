# Jetson Nano Setup

## Setup Swap File
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

## Setup Docker
เชื่อมต่อ MicroUSB Cable เชื่อมต่อระหว่างคอมพิวเตอร์กับ Jetson Nano และต่อ Jetson Nano เข้ากับสาย Ethernet

ล็อกอินเข้า Jetson Nano แล้วสร้าง Directory เพื่อใช้เก็บข้อมูลด้วยคำสั่ง
```
mkdir -p ~/nvdli-data
```

ติดตั้ง docker image ด้วยคำสั่ง
```
echo "sudo docker run --runtime nvidia -it --rm --network host \
   --volume ~/nvdli-data:/nvdli-nano/data \
   --device /dev/video0 \
   nvcr.io/nvidia/dli-nano-ai:v2.0.2-r32.7.1" > docker_dli_run.sh

chmod +x docker_dli_run.sh
./docker_dli_run.sh
```

จากนั้นสามารถเปิดเว็บ http://192.168.55.1:8888 โดยพาสเวิร์ดคือ dlinano

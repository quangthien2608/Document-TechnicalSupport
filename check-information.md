# Ubuntu
**1.Kiểm tra server** </br> <p>Lệnh kiểm tra phiên bản: ```lsb_release -a```</p>
**Kiểm tra tài nguyên :**
- **CPU** 
``` 
cat /proc/cpuinfo | grep processor 
```
- **RAM** 
```
cat /proc/meminfo | grep -i memtotal
```
- **Disk**
```
df -h
```
- **Speedtest**
Lệnh cài đặt speedtest:
```
apt install -y speedtest-cli
```
Lấy danh sách ISP: 
```
speedtest-cli –secure –list | grep Vietnam
```
Kiểm tra Bandwith:
```
speedtest-cli –secure –server *
```
**chú thích**: (*) ở đây mà số ID của ISP ở danh sách trước đó
- **Kiểm tra đọc/ghi ổ đĩa** 
Lệnh cài đặt hdparm:
```
apt install hdparm
```
Kiểm tra:
```
sudo hdparm -Tt /dev/sda
```
**chú thích**: "/dev/sda/" ở đây là ổ đĩa cần kiểm tra

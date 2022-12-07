# Ubuntu
**1.Kiểm tra server** </br> <p>Lệnh kiểm tra phiên bản: ```lsb_release -a```</p>
**Kiểm tra tài nguyên :**
- **CPU** <p>``` cat /proc/cpuinfo | grep processor ```</p>
- **RAM** <p>```cat /proc/meminfo | grep -i memtotal```</p>
- **Disk**<p> ```df -h```</p>
- **Speedtest** <p>Lệnh cài đặt speedtest: ```apt install -y speedtest-cli```</p> <p>Lấy danh sách ISP: ```speedtest-cli –secure –list | grep Vietnam```</p> <p>Kiểm tra Bandwith: ```speedtest-cli –secure –server *``` | **chú thích**: (*) ở đây mà số ID của ISP ở danh sách trước đó</p>
- **Kiểm tra đọc/ghi ổ đĩa** <p>Lệnh cài đặt hdparm: ```apt install hdparm```</p>  <p>Kiểm tra: ```sudo hdparm -Tt /dev/sda``` | **chú thích**: "/dev/sda/" ở đây là ổ đĩa cần kiểm tra</p>

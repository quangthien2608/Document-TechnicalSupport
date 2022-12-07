# CentOS 7
**Cách 1: Cấu hình theo file config** <p>Kiểm tra thông tin eth:</p> 
```
ip a
``` 
Cấu hình: 
```
vi /etc/sysconfig/network-scripts/ifcfg-eth0
```
chú thích: "ifcfg-**eth0**" là card mạng đã kiểm tra trước đó.
```
DEVICE= eth0			#Tên card mạng
NAME= eth0			#Tên card mạng
ONBOOT = yes			#Sau khi reboot, Network sẽ được on với cấu hình mạng tương ứng 
BOOTPROTO = none		#Cấu hình dhcp thì giá trị là dhcp, ip tĩnh thì để = none
IPADDR = 192.168.1.10		#Địa chỉ ip muốn gán
NETMASK = 255.255.255.0	#Subnet mask của lớp mạng ip sử dụng
GATEWAY = 192.168.1.1	#Địa chỉ gateway
DNS1 = 8.8.8.8			#Địa chỉ DNS server
DNS2 = 8.8.4.4 			#Địa chỉ DNS server 
```
Khởi động lại network để có hiệu lực: 
```
systemctl restart network
```
kiểm tra lại ip 
```
ip a
```
</br> </br>
**Cách 2: Cấu hình bằng nmtui** <br>
Mở **nmtui**: 
```
nmtui
``` 
sau đó chọn **Edit a connection** tiếp theo chọn eth máy chủ có và cần cấu hình đặt **IP, GATEWAY, DNS** </br>
Sau khi cầu hình hoàn tất lưu và thoát khởi động lại network.

# Ubuntu 20.04

Cấu hình file: 
```
nano /etc/netplan/00-installer-config.yaml
``` 
Sau đó tiến hành chỉnh sửa IP, GATEWAY, DNS </br>
Sau khi chỉnh sửa hoàn tất nhập lệnh: 
```
netplan apply
``` 
để khởi động lại cấu hình. </br>
- **Chú ý**: Nếu file cấu hình chưa có ta có thể truy cập **/etc/netplan** để kiểm tra xem có file mặc định hay không nếu có copy ra file mới để cấu hình.</br>
- **Ví dụ:**
```
cp /etc/netplan/99-installer-config.yaml /etc/netplan/00-installer-config.yaml
```

# CentOS 7
**Cách 1: Cấu hình theo file config** </br> <p>Kiểm tra thông tin eth: ```ip a```</p> Cấu hình: ```vi /etc/sysconfig/network-scripts/ifcfg-eth0``` | chú thích: "ifcfg-**eth0**" là card mạng đã kiểm tra trước đó.
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
Khởi động lại network để có hiệu lực: ```systemctl restart network``` và kiểm tra lại ip ```ip a```

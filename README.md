# Mục lục
- [OS Ubuntu](#os-ubuntu)

# SSH
- **Syntax**
```
ssh user@ip -p port
```
Run with port default 21
```
ssh root@192.168.1.22
```
Run with port 221
```
ssh root@192.168.22 -p 221
```

# Remove file with Inodes 
check indodes
``
ls -i <dir_name>
``
or
``
stat <file_name>
``
</br> </br>
**Remove file with Inodes**
```
find . -inum <inode-number> -exec rm -i {} \;
```
#
# Các lệnh và cú pháp tìm trong Linux

- **Cú pháp(Syntax)**
```
find command options starting/path expression
```
- **Tìm kiếm** </br>
trong thư mục **/var/www/** và định dạng đuôi tập tin **.html**
```
find -O3 -L /var/www/ -name "*.html"
```
tập tin trong thư mục con
```
find . -name thisfile.txt
```
tất cả các file có trong đường dẫn hiện tại | ví dụ: **/home**
```
find . -type f -empty
```
tại thời điểm tập tin được sửa đổi (trong vòng "**số ngày**" sửa đổi trước đó)
```
find / -name "*jpg" -mtime 5
find /home/randomuser/ -name "*jpg" -mtime 4
```
sử dụng thêm grep để tìm
```
find / -name "*jpg" -mtime 4 | grep site
```
#
# [OS Ubuntu](#os-ubuntu)
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
#
# Command
- **Clear memory cache**
```
sudo -i
sync; echo 1 > /proc/sys/vm/drop_caches 
```
- **Check ram**
```
sudo free -m
```
#

# Extend trên CentOS7 + Ubuntu16 1Disk không cần reboot server:
```
yum install -y parted #Centos
```
```
apt-get install -y parted #Ubuntu
```
******************************************
**TH1: CentOS7**

- Thường thì sẽ 1 disk sda    /dev/sda
**Lệnh xem:**    
```
fdisk -l hoặc lsblk -l
```
```
 Primary partition:
    /dev/sda 
    /dev/sda1     dành cho boot 
    /dev/sda2     dành cho phân vùng /
```
- Tiến hành extend vào sda2:
```
fdisk -l /dev/sda | grep ^/dev 
```
```
# parted /dev/sda 
# resizepart 2 100%      | mình extend partition 2 (sda2) 100%
# quit
```
Check 
```
fdisk -l 
```
hoặc 
```
pvscan
```
xem dung lượng partition sda2 đã được tăng lên chưa.

- Tiếp tục dùng lệnh sau để exten vào volume group /
```
# pvresize /dev/sda2
# lvresize --extents +100%FREE --resizefs /dev/mapper/centos-root
```
- Check lại: 
```
df -h #Kiểm tra dung lượng
```
******************************************
**TH2: Ubuntu** </br>
Thường thì sẽ 1 disk sda    /dev/sda </br>
**Lệnh xem:**
```
fdisk -l 
```
hoặc 
```
lsblk -l
```
```
Extended partition:
/dev/sda 
/dev/sda1     dành cho boot 
/dev/sda2     dành cho phân vùng /
/dev/sda5     Logical partition của /sda2       
```
- Tiến hành extend vào Extended sda2 và Logical sda5
```
fdisk -l /dev/sda | grep ^/dev 		
```
```
#parted /dev/sda 

#resizepart 2 100%      | mình exten  partition 2 (sda2) 100%

#resizepart 5 100%      | mình exten  Logical 5 (sda5) 100%

#quit
```
```
fdisk -l
```
hoặc
```
pvscan
```
xem dung lượng partition sda2 và sda5 đã được tăng lên chưa.

- Tiếp tục dùng lệnh sau để exten vào volume group /
```
pvresize /dev/sda2
```
```
pvresize /dev/sda5
```
```
lvresize --extents +100%FREE --resizefs /dev/mapper/ubuntu--vg-root
```
```
lvresize --extents +100%FREE --resizefs /dev/mapper/ubuntu--vg-ubuntu--lv
```

******************************************
**GrowPart**

Trường hợp này có thể áp dụng exten 1 disk trên cả CentOS6,7 + Ubuntu16,14
</br>
Tuy nhiên Centos6 phải reboot lại.

- GrowPart
**CentOS / RHEL:**
```
yum install cloud-utils-growpart #Install
```
**Ubuntu / Debian:**
```
apt-get install cloud-guest-utils #Install
```
- Dùng growpart resize partition
```
growpart /dev/[Device Name] [Partition Numner]
```
```
growpart /dev/sda 2       #exten vào sda2
```
```
fdisk -l
```
hoặc 
```
pvscan
```
xem dung lượng partition sda2 đã được tăng lên chưa.
</br>
Tiếp tục dùng lệnh sau để exten vào volume group /
```
pvresize /dev/sda2
```
```
lvresize --extents +100%FREE --resizefs /dev/mapper/cl-root
```

******************************************

```
pvresize /dev/sda5
```
```
lvextend /dev/ubuntu-vg/root /dev/sda5
```
```
resize2fs /dev/ubuntu-vg/root      #CentOS6
```
```
xfs_growfs /dev/Mega/root          #CentOS7 
```

******************************************
# 
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
- Tạo file config mặc định
```
# This file describes the network interfaces available on your system
# For more information, see netplan(5).
network:
  version: 2
  renderer: networkd
  ethernets:
    enp3s0f0:
      dhcp4: no
      addresses: [192.168.45.13/24]       
      gateway4: 192.168.45.1              
      nameservers:
          addresses: [1.1.1.1,8.8.8.8]
```
#
# Firewall Ubuntu
**Configure file location**
```
sudo nano /etc/default/ufw
```
Edit
```
IPV6=yes
```

**Deny incoming & allow outgoing**
```
sudo ufw default deny incoming
sudo ufw default allow outgoing
```

**Allow SSH connection**
```
sudo ufw allow ssh
```
or
```
sudo ufw allow 22
```
**SSH with port 2222***
```
sudo ufw allow 2222
```

**Enable UFW**
```
sudo ufw enable
```

**Allow some connection**
**HTTP - 80**
```
sudo ufw allow http
```
or
```
sudo ufw allow 80
```

**HTTPS - 443**
```
sudo ufw allow https
```
or
```
sudo ufw allow 443
```

**Range 6000:6007/tcp & udp**
```
sudo ufw allow 6000:6007/tcp
sudo ufw allow 6000:6007/udp
```

**IP**
```
sudo ufw allow from 203.0.113.4
```
**IP connection with port 22 SSH**
```
sudo ufw allow from 203.0.113.4 to any port 22
```

**Subnets**
```
sudo ufw allow from 203.0.113.0/24
sudo ufw allow from 203.0.113.0/24 to any port 22
```

**Network Interface**
```
sudo ufw allow in on ens3 to any port 80
sudo ufw allow in on eth1 to any port 3306
```

**Denying Connections**
```
sudo ufw deny http
sudo ufw deny from 203.0.113.4
```

**Deleteing Rules**
```
sudo ufw status numbered
```
```
sudo ufw delete 2
```
**By Actual Rule**
```
sudo ufw delete allow http
sudo ufw delete allow 80
```
**Checking UFW Status and Rules**
```
sudo ufw status verbose
```
**Disabling or Resetting UFW**
**Disable**
```
sudo ufw disable
```
**Reset**
```
sudo ufw reset
```
#
# Firewalld Cent 7

**check status**
```
systemctl status firewalld
systemctl is-active firewalld 
firewall-cmd --state
```
**startup boot**
```
systemctl enable firewalld
systemctl is-enabled firewalld     #check
```
**restart**
```
systemctl restart firewalld
firewall-cmd --reload
```
**stop & disabled**
```
systemctl stop firewalld
systemctl disable firewalld
```
**config zones**
```
firewall-cmd --get-zones      #check list zones
firewall-cmd --get-default-zone     #check zone default
firewall-cmd --get-active-zones     #check zone active
firewall-cmd --set-default-zone-home  #set default zone home
firewall-cmd --zone=home --list-all   #check all rule of zone
firewall-cmd --zone=public --list services    #check services
firewall-cmd --zone=public --list-ports       #check ports
```
**identify services on system***
```
firewall-cmd --get-services
```

**disabled serivces on firewalld**
```
firewall-cmd --zone=public --remove-service=http
firewall-cmd --zone=public --remove-service=http  --permanent
```
**configure for port**
```
firewall-cmd –zone=public –add-port=80/tcp 
firewall-cmd –zone=public –add-port=80/tcp --permanent
```
**open range port**
```
firewall-cmd –zone=public –add-port=35000-40000/tcp
```
**close**
```
firewall-cmd --zone=public --remove-port=9999/tcp
firewall-cmd --zone=public --remove-port=9999/tcp --permanent
```
**create zone private**
```
firewall-cmd –permanent –new-zone=publicweb
firewall-cmd –permanent –new-zone=publicweb 
firewall-cmd –reload 
firewall-cmd –get-zones
```

**create services on firewalld**
- copy configure default & edit
```
cp /usr/lib/firewalld/services/ssh.xml /etc/firewalld/services/configurefirewall-admin.xml
nano /etc/firewalld/services/configurefirewall-admin.xml
```
![image](https://user-images.githubusercontent.com/69961900/208356939-a2b2f15b-7f8c-4980-bf5d-8b0898cdf690.png)
```
firewall-cmd –reload
```
**check list services**
```
firewall-cmd –get-services
```
**start services**
```
firewall-cmd –zone=public –add-services=configurefirewall-admin
firewall-cmd –zone=public –add-services=configurefirewall-admin –permanent
```
#
# Cài đặt Directadmin trên CentOS 7 & 8
- **Update Server và cài đặt các gói cần thiết** </br>
Bạn cần đăng nhập bằng tài khoản root. Nhưng nếu đăng nhập bằng tài khoản khác thì dùng lệnh su để chuyển sang tài khoản root, nhưng nhớ thêm dùng **“AllowUsers username”** vào file **“/etc/ssh/sshd_config”** nếu không thì khi cài đặt xong bạn không thể truy cập vào được nữa mà phải cài lại OS.
```
yum -y update
```
**Cài đặt net-tools**
```
yum install -y wget net-tools
```
**Xóa ứng dụng postfix được cài đặt sẵn trên server**
```
yum remove -y postfix
```

- **Cài đặt các gói cần thiết**
```
yum install wget gcc gcc-c++ flex bison make bind bind-libs bind-utils openssl openssl-devel perl quota libaio
libcom_err-devel libcurl-devel gd zlib-devel zip unzip libcap-devel cronie bzip2 cyrus-sasl-devel perl-ExtUtils-Embed
autoconf automake libtool which patch mailx bzip2-devel lsof glibc-headers kernel-devel expat-devel -y
```
``` 
yum -y install psmisc net-tools systemd-devel libdb-devel perl-DBI xfsprogs rsyslog logrotate crontabs file
```

**Chỉnh lại hostname**
```
hostnamectl set-hostname hosting82198.lvs
```
**Chỉnh dns LongVan sang Google DNS**
```
vi /etc/sysconfig/network-scripts/ifcfg-ens192
```

**Tải gói cài đặt DA và cấp quyền cho file cài đặt**
```
wget http://www.directadmin.com/setup.sh
chmod 755 setup.sh
```

- **Chạy tập lệnh cài đặt DirectAdmin**
```
./setup.sh
```
Gõ y và nhấn Enter để cài đặt các gói cần thiết.

Điền Client ID, License ID và hostname. Các thông tin về Client ID, License ID, bạn cần điền chính xác bởi nếu không khi cài đặt sẽ báo lỗi bản quyền.

Lưu ý rằng hostname không được giống với tên miền chính. 

Các câu hỏi tiếp theo thì bạn tiếp tục nhấn y và nhấn Enter.

Bây giờ thì chỉ cần đợi từ 25-35 phút để việc cài đặt hoàn tất. Nếu thành công, bạn sẽ nhận được thông báo sau: 

Sau khi cài đặt xong, bạn thử đăng nhập vào link với tài khoản hiển thị trên màn hình. Nếu không chạy thì bạn phải chạy thêm các lệnh để mở port cho firewall với câu lệnh sau: 
```
firewall-cmd --zone=public --add-port=2222/tcp --permanent
firewall-cmd --zone=public --add-port=21/tcp --permanent
firewall-cmd --zone=public --add-port=80/tcp --permanent
firewall-cmd --zone=public --add-port=25/tcp --permanent
firewall-cmd --reload
```
```
systemctl restart directadmin
```
- đối với gói datacenter thì tạo thêm card mạng ảo với ip public k gateway 
sau đó vào 
```
vi /usr/local/directadmin/conf/directadmin.conf 

lan_ip = ip private(172......)
```
#
# Cài đặt Directadmin trên Ubuntu 20.04
**Cập nhật các package**
```
sudo apt update
```

**Cài đặt net-tools**
```
apt install -y wget net-tools
```
**Xóa ứng dụng postfix được cài đặt sẵn trên server**
```
apt install -y remove postfix
```

**Cài đặt các package cần thiết**
```
sudo apt install wget gcc g++ make flex bison openssl libssl-dev 
sudo apt install perl perl-base perl-modules libperl-dev libperl4-corelibs-perl
sudo apt install libwww-perl libaio1 libaio-dev zlib1g zlib1g-dev libcap-dev cron
sudo apt install bzip2 zip automake autoconf libtool cmake pkg-config python
sudo apt install libdb-dev libsasl2-dev libncurses5 libncurses5-dev libsystemd-dev
sudo apt install bind9 dnsutils quota patch logrotate rsyslog libc6-dev libexpat1-dev
sudo apt install libcrypt-openssl-rsa-perl curl libnuma-dev libnuma1
```

**Chỉnh lại hostname**
```
hostnamectl set-hostname hosting82198.lvs
```
**Chỉnh dns LongVan sang Google DNS**
```
nano /etc/netplan/99-netcfg-vmware.yaml
```

**Tải gói cài đặt DA và cấp quyền cho file cài đặt**
```
wget http://www.directadmin.com/setup.sh
chmod 755 setup.sh
```

**Tiến hành cài đặt**
```
# ./setup.sh cPUZqL4O0elZziPXZdbMLMPy1f1b6HsYe7mCFoz/L60=
```
Với dãy ``cPUZqL4O0elZziPXZdbMLMPy1f1b6HsYe7mCFoz/L60=`` là license key hash mà các anh sẽ gửi.

**Sau khi hoàn tất đặt lại mật khẩu truy cập**
```
passwd admin
```
Kiểm tra đăng nhập panel directadmin với đường dẫn http://ip:2222 và login user admin vào.
#
# Cài đặt PHP, PHPMyAdmin
Lệnh cài đặt:
```
apt install -y php*
```
```
apt install -y phpmyadmin php*-mbstring php*-zip php*-gd php*-json php*-curl
```
Chú thích: "*" ở đây là số phiên bản php ta cần cài đặt để tránh xảy không đúng phiên bản cần cài đặt
#
# MariaDB Tips
- **Truy cập**
```
mysql -u root -p
```
>- **Nếu gặp lỗi** ```'Access denied for user 'root'@'localhost' (using password: YES)'``` </br>
>1. **Mở và chỉnh sửa** ```/etc/my.cnf``` hoặc ```/etc/mysql/my.cnf``` tùy thuộc vào cấu hình của bạn. </br>
>2. **Bổ sung nội dung**
>  ```
>  [mysqld]
>  skip-grant-tables
>  ```
>3. **Khởi động lại MySQL** ```systemctl restart mysql```
>4. Đã có thể đăng nhập vào MySQL ngay bây giờ bằng lệnh ```mysql -u root -p```
>5. Chạy lệnh ```mysql> FLUSH PRIVILEGES;```
>6. Đặt mật khẩu mới bằng cách dùng lệnh bên dưới
>- **MariaDB 5.7.6 hoặc mới hơn**
>```
>ALTER USER 'root'@'localhost' IDENTIFIED BY 'newpassword';
>```
>- **MariaDB 5.7.5 hoặc cũ hơn**
>```
>SET PASSWORD FOR 'root'@'localhost' = PASSWORD('newpassword');
>```
>7. Quay trở lại **/etc/my.cnf** và xóa nội dung đã thêm ở mục 2.
>8. Khởi động lại MySQL
>9. Bây giờ đã có thể đăng nhập bằng mật khẩu mới ```mysql -u root -p```
- **Tạo cơ sở dữ liệu mới**
```
CREATE DATABASE DATABASE_NAME;
```
- **Tạo người dùng mới (chỉ có quyền cục bộ) và cấp đặc quyền cho người dùng trên cơ sở dữ liệu mới**
```
GRANT ALL PRIVILEGES ON DATABASE_NAME.* TO 'USER_NAME'@'localhost' IDENTIFIED BY 'PASSWORD';
```
- **Tạo người dùng mới (có quyền truy cập từ xa) và cấp đặc quyền cho người dùng trên cơ sở dữ liệu mới**
```
GRANT ALL PRIVILEGES ON DATABASE_NAME.* TO 'USER_NAME'@'%' IDENTIFIED BY 'PASSWORD';
```
- **Sau sửa đổi, thực hiện lệnh sau để áp dụng các thay đổi**
```
FLUSH PRIVILEGES;
```
******************************************
- **Sửa lỗi không khởi động được dịch vụ**
```
sudo chmod 755 /var/lib/mysql/mysql
```
#
# OwnCloud - Rclone mount S3 Storage
**update & upgrade OS**
```
apt-get update
apt-get upgrade
```
**install docker**
```
curl -fsSL https://get.docker.com -o get-docker.sh
sh get-docker.sh
```
**check version**
```
docker -v
```
**enable startup**
```
systemctl enable docker
```
**install docker-rcompose**
```
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```
**check version**
```
docker-compose --version
```
**install rclone + s3**
```
curl https://rclone.org/install.sh | sudo bash
```
**rclone config**
```
rclone config
```
**config file "/root/.config/rclone/rclone.conf" not found - using defaults </br> No remotes found, make a new one?**
```
n) new remote
s) set configuration password 
q) quit config  
n/s/q> n

Enter name for new remote
name> s3

5 / Amazon S3 Compliant Storage Providers including AWS, Alibaba, Ceph, China Mobile, Cloudflare...
Storage> 5

provider> 24
env_auth>
access_key_id> input access key
secret_access_key> input secret access key
endpoint> s3-hcm-r1.longvan.net
location_constraint>
acl> 1

Edit advanced config?
y) Yes
n) No (default)
y/n> n

Keep this "s3" remote?
y) Yes this is OK (default)
e) Edit this remote
d) Delete this remote
y/e/d> y

```

**mount S3 config including Rclone**
**create folder S3 data mount s3 rclone**
```
mkdir –p /home/owncloud/own_data/files/
```
**create service rclone**
```
cd /etc/systemd/system/ 
wget https://s3-hcm1-r1.longvan.net/testing/rclone.txt
cp -r rclone.txt rclone.service
```
Environment=MOUNT_DIR=/home/owncloud/own_data/files/ is folder sync data server s3 rclone
```
systemctl restart daemon-reload
systemctl restart rclone
systemctl enable rclone
```
**create folder data owncloud**
```
mkdir -p /home/owncloud/own_data/db/
mkdir -p /home/owncloud/own_data/redis/
```

**create folder containt file install owncloud docker compose**
```
mkdir -p /home/owncloud/own_installer/own/
cd /home/owncloud/own_installer/own/
```
**get file docker-compose.yml**
```
wget https://s3-hcm1-r1.longvan.net/testing/docker-compose.yml
```
**create the environment configuration file**
```
cat << EOF > .env
OWNCLOUD_VERSION=10.11
OWNCLOUD_DOMAIN=localhost:8080
OWNCLOUD_TRUSTED_DOMAINS=IP server current using
ADMIN_USERNAME=admin
ADMIN_PASSWORD=admin
HTTP_PORT=8080
EOF
```

**installing**
```
cd /home/owncloud/own_installer/own/
docker-compose up -d
```
**check access owncloud** </br>
http://{your ip}:8080
#
# CSF FW
- **Open a Port in CSF Firewall** </br>
**Open the configuration file of the CSF as follows.**
```
vi /etc/csf/csf.conf
```
**Add the required ports to the csf.conf file**
```
# Allow incoming TCP ports

TCP_IN = “20,21,22,25,26,53,80,110,143,443,465,587,993,995”

# Allow outgoing TCP ports

TCP_OUT = “20,21,22,25,26,37,43,53,80,110,113,443,465,873”
```
**Restart the CSF for the changes to take effect. Run the below command to restart the CSF.**
```
csf -r 
```

| Command	 | Description	 | Example |
| :---         |     :---      |          :--- |
| csf -e	   | Enable CSF	     | root@server[~]#csf -e    |
| csf -x	     | Disable CSF	      | root@server[~]#csf -x      |
| csf -s	   | Start the firewall rules	     | root@server[~]#csf -s    |
| csf -f	     | Flush/Stop firewall rules (note: lfd may restart csf)| root@server[~]#csf -f      |
| csf -r	   | Restart the firewall rules	     | root@server[~]#csf -r    |
| csf -a [IP.add.re.ss] [Optional comment]	     | Allow an IP and add to /etc/csf/csf.allow       | root@server[~]#csf -a 187.33.3.3 Home IP Address      |
| csf -td [IP.add.re.ss] [Optional comment]	   | Place an IP on the temporary deny list in /var/lib/csf/csf.tempban	     |root@server[~]#csf -td 55.55.55.55 Odd traffic patterns    |
| csf -tr [IP.add.re.ss]	     | Remove an IP from the temporary IP ban or allow list.| root@server[~]#csf -tr 66.192.23.1      |
| csf -tf	   | Flush all IPs from the temporary IP entries   | root@server[~]#csf -tf    |
| csf -d [IP.add.re.ss] [Optional comment]	     | Deny an IP and add to /etc/csf/csf.deny	       | root@server[~]#csf -d 66.192.23.1 Blocked This Guy      |
| csf -dr [IP.add.re.ss]	   | Unblock an IP and remove from /etc/csf/csf.deny	     | root@server[~]#csf -dr 66.192.23.1   |
| csf -df    | Remove and unblock all entries in /etc/csf/csf.deny	      | root@server[~]#csf -df      |
| csf -g [IP.add.re.ss]   | Search the iptables and ip6tables rules for a match (e.g. IP, CIDR, Port Number)	       | root@server[~]#csf -g 66.192.23.1      |
| csf -t    |  Displays the current list of temporary allow and deny IP entries with their TTL and comments	       |  root@server[~]#csf -t      |
#
# Dirty bit
- **Cú pháp**
```
fsutil dirty {query | set} <volumepath>
```

- **Kiểm tra**
```
fsutil dirty query c:
```
>bị Dirty bit ```Volume C: is dirty``` </br>
>không bị dirty bit ```Volume C: is not dirty```
*****************************
- **Sửa lỗi** </br>
```
chkdsk D: /f
```
Hoặc
```
chkdsk D: /x
```

Tham khảo: https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/chkdsk?tabs=event-viewer
#
# Autoruns for Windows
https://learn.microsoft.com/en-us/sysinternals/downloads/autoruns
*****************************
# RAMMap
https://learn.microsoft.com/en-us/sysinternals/downloads/rammap
#

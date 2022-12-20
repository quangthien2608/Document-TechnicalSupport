# Cài đặt Directadmin trên CentOS 7 & 8
- **Update Server và cài đặt các gói cần thiết** </br>
Bạn cần đăng nhập bằng tài khoản root. Nhưng nếu đăng nhập bằng tài khoản khác thì dùng lệnh su để chuyển sang tài khoản root, nhưng nhớ thêm dùng **“AllowUsers username”** vào file **“/etc/ssh/sshd_config”** nếu không thì khi cài đặt xong bạn không thể truy cập vào được nữa mà phải cài lại OS.
```
yum -y update
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
- **Tải tập tin setup.sh**
```
wget http://www.directadmin.com/setup.sh
```
- **Thay đổi quyền trên file setup.sh**
```
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


# Cài đặt Directadmin trên Ubuntu 20.04

```
sudo apt update
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

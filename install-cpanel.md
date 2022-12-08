# CentOS

- **Tắt SELINUX**
```
echo SELINUX=disabled >> /etc/selinux/config
```
hoặc mở tập tin cấu hình ```vi /etc/sysconfig/selinux``` và thêm nội dung bên dưới 
```
SELINUX=enforecing –>disable
```
- **Vô hiệu hóa Firewalld**
```
systemctl stop firewalld
systemctl disable firewalld
```
- **Cập nhật hệ thống**
```
yum -y update
```
- **Tắt network manager**
```
systemctl stop NetworkManager.service
systemctl disable NetworkManager.service
systemctl enable network.service
systemctl start network.service
```
- **Tải và cài đặt cPanel**
```
cd /home && curl -o latest -L https://securedownloads.cpanel.net/latest && sh latest
```
Hoàn tất và truy cập đường dẫn ```http://{ip}:2083```

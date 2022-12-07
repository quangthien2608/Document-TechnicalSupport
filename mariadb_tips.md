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
>6. Đặt mật khẩu mới bằng cách ```ALTER USER 'root'@'localhost' IDENTIFIED BY 'newpassword';```
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

# MariaDB Tips
- **Tạo cơ sở dữ liệu mới**
```
MariaDB> CREATE DATABASE DATABASE_NAME;
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

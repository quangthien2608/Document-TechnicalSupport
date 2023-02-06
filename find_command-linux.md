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

**Tham khảo**: https://www.plesk.com/blog/various/find-files-in-linux-via-command-line/

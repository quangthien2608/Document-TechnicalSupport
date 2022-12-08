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

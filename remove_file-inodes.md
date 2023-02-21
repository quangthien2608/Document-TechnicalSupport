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

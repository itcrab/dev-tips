# Bash tips

### Download file by SSH
```Bash
scp root@domain:/root/filename.ext .
```

### Write to top of file
```Bash
echo "
text top of file - line 1
text top of file - line 2
$(cat /path/to/file)" >/path/to/file
```

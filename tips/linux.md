# Linux tips

### Unban IP from fail2ban :)
```Bash
fail2ban-client -i
status sshd  # IP in ban list
set sshd unbanip 127.0.0.1
status sshd  # IP not in ban list
```

### Creating SWAP
```Bash
fallocate -l 8G /swapfile
chmod 600 /swapfile
mkswap /swapfile
swapon /swapfile
echo "/swapfile   none    swap    sw    0   0">>/etc/fstab
echo "
vm.swappiness = 10
vm.vfs_cache_pressure = 50
">>/etc/sysctl.conf
```

### Linux details info
```Bash
uname -a
cat /etc/os-release
```

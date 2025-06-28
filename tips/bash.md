# Bash tips

### Generate password
```Bash
openssl rand -hex 32
```

### Generate SSH-key
```Cmd
ssh-keygen -b 4096 -t rsa -C "name@mail.com" -N mypassphrase -f server-name
```

### Open ports status
```Bash
ss -ntpl
State  Recv-Q Send-Q Local Address:Port Peer Address:PortProcess
LISTEN 0      128          0.0.0.0:1234      0.0.0.0:*    users:(("username",pid=1001,fd=1))
LISTEN 0      128                *:22              *:*    users:(("sshd",pid=1002,fd=2),("systemd",pid=1003,fd=3))
```

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

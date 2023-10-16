# Docker tips

### `elasticsearch` container `vm.max_map_count` error in Docker by Windows 10/11 WSL2
```Bash
# bootstrap check failure [1] of [1]: max virtual memory areas vm.max_map_count [65530] is too low, increase to at least [262144]
wsl.exe -u root
sysctl -w vm.max_map_count=262144
exit
```

### Remove some networks
```Bash
$ docker network ls
...
$ docker network rm 93319239b924
$ docker network rm 9406a7197e73
```

### Remove all docker images
```Bash
docker rmi $(docker images -a -q)
```

### Remove all docker volumes
```Bash
docker volume rm $(docker volume ls -qf dangling=true)
```

### Remove unused data
```Bash
docker system prune -a -f
```

### Docker-compose up
```Bash
docker-compose -f docker-compose.yml up -d --build
```

### Dockerfile - create file from base64 string
```Bash
RUN echo "base64string==" | base64 -d | tee >/file.sh
```

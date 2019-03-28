# Docker tips

### Remove all docker images
```Bash
docker rmi $(docker images -a -q)
```

### Remove all docker volumes
```Bash
docker system prune -a -f
docker volume rm $(docker volume ls -qf dangling=true)
```

### Docker-compose up
```Bash
docker-compose -f docker-compose.yml up -d --build
```

### Dockerfile - create file from base64 string
```Bash
RUN echo "base64string==" | base64 -d | tee >/file.sh
```

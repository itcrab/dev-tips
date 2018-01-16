# Docker tips

### Docker-compose up
```Bash
docker-compose -f docker-compose.yml up -d --build
```

### Dockerfile - create file from base64 string
```Bash
RUN echo "base64string==" | base64 -d | tee >/file.sh
```

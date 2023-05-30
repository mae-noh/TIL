# Docker 기본 명령어

###
```
docker ps
```

```
docker images
```

### 모든 컨테이너 Stop
```
docker stop $(docker ps -a -q)
```

### 모든 컨테이너 Remove
```
docker rm $(docker ps -a -q)
```

# Cerebro설치

## Cerebro 패키지 다운로드
```
curl -LO https://github.com/lmenezes/cerebro/releases/download/v{버전}/cerebro-{버전}.tgz

tar -xzf cerebro-{버전}.tgz
```

## application.conf 설정
/conf/application.conf <br>
모니터링할 ES 정보 설정

```
hosts = {
    host = "host:port",
    name = "name"
}
```
- host:port 모니터링할 ES 정보
  - host http://<IP>
- name cerebro에서 해당 host에 설정되는 이름

# ES secutiry 설정

## 최소 보안설정

<b>elasticsearch</b>
- bin/elasticsearch.yml
  ```
  xpack.security.enabled: true
  xpack.security.authc.api_key.enabled: true // API keys 설정
  ```
- elasticsearch 실행
- 비밀번호 변경
  bin/elasticsearch-setup-passwords interactive

<b>kibana</b>
- bin/kibana.yml 파일 설정 변경
  ```
  elasticsearch.username: "kibana_system"
  ```
- elasticsearch 비밀번호 설정
  ```
  bin/kibana-keystore create
  bin/kibana-keystore add elasticsearch.password
  ```
- kibana 실행

## Slack Webhook 만들기
- slack에서 Incomming WebHooks 다운
- channel 선택
- Example을 복사하여 터미널에 입력하여 실행
- slack의 선택한 channel에 테스트 요청한 메시지 확인

## Alerts
<b>Rules and Connectors</b>

## SSL 설정
./bin/elasticsearch-certutil ca

파일 저장 위치 enter<br>
비밀번호 입력<br>

```
xpack.security.transport.ssl.keystore.path: /etc/elasticsearch/certs/elastic-certificates.p12<br>
xpack.security.transport.ssl.truststore.path: /etc/elasticsearch/certs/elastic-certificates.p12<br>
xpack.security.http.ssl.keystore.path: /etc/elasticsearch/certs/elastic-certificates.p12<br>
xpack.security.http.ssl.truststore.path: /etc/elasticsearch/certs/elastic-certificates.p12<br>
```

```
xpack.security.transport.ssl.keystore.password: <your_password_here><br>
xpack.security.transport.ssl.truststore.password: <your_password_here><br>
xpack.security.http.ssl.keystore.password: <your_password_here><br>
xpack.security.http.ssl.truststore.password: <your_password_here><br
```
or 
```
./elasticsearch-keystore add xpack.security.transport.ssl.keystore.secure_password<br>
./elasticsearch-keystore add xpack.security.transport.ssl.truststore.secure_password<br>
./elasticsearch-keystore add xpack.security.http.ssl.keystore.secure_password<br>
./elasticsearch-keystore add xpack.security.http.ssl.truststore.secure_password<br>
```

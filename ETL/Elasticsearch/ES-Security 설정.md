#ES Secutiry 설정


./bin/elasticsearch-certutil ca

파일 저장 위치 enter
비밀번호 입력

xpack.security.transport.ssl.keystore.path: /etc/elasticsearch/certs/elastic-certificates.p12<br>
xpack.security.transport.ssl.truststore.path: /etc/elasticsearch/certs/elastic-certificates.p12<br>
xpack.security.http.ssl.keystore.path: /etc/elasticsearch/certs/elastic-certificates.p12
xpack.security.http.ssl.truststore.path: /etc/elasticsearch/certs/elastic-certificates.p12



xpack.security.transport.ssl.keystore.password: <your_password_here>
xpack.security.transport.ssl.truststore.password: <your_password_here>
xpack.security.http.ssl.keystore.password: <your_password_here>
xpack.security.http.ssl.truststore.password: <your_password_here>



./elasticsearch-keystore add xpack.security.transport.ssl.keystore.secure_password
./elasticsearch-keystore add xpack.security.transport.ssl.truststore.secure_password
./elasticsearch-keystore add xpack.security.http.ssl.keystore.secure_password
./elasticsearch-keystore add xpack.security.http.ssl.truststore.secure_password

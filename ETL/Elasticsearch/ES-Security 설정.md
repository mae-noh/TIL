#ES Secutiry 설정


./bin/elasticsearch-certutil ca

파일 저장 위치 enter<br>
비밀번호 입력<br>

xpack.security.transport.ssl.keystore.path: /etc/elasticsearch/certs/elastic-certificates.p12<br>
xpack.security.transport.ssl.truststore.path: /etc/elasticsearch/certs/elastic-certificates.p12<br>
xpack.security.http.ssl.keystore.path: /etc/elasticsearch/certs/elastic-certificates.p12<br>
xpack.security.http.ssl.truststore.path: /etc/elasticsearch/certs/elastic-certificates.p12<br>



xpack.security.transport.ssl.keystore.password: <your_password_here><br>
xpack.security.transport.ssl.truststore.password: <your_password_here><br>
xpack.security.http.ssl.keystore.password: <your_password_here><br>
xpack.security.http.ssl.truststore.password: <your_password_here><br

or 

./elasticsearch-keystore add xpack.security.transport.ssl.keystore.secure_password<br>
./elasticsearch-keystore add xpack.security.transport.ssl.truststore.secure_password<br>
./elasticsearch-keystore add xpack.security.http.ssl.keystore.secure_password<br>
./elasticsearch-keystore add xpack.security.http.ssl.truststore.secure_password<br>

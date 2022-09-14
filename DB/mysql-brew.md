# MacOS 로 MySql 설치 및 실행

brew update<br>
brew install mysql<br>
mysql --version<br>

### 실행 및 종료
- 데몬모드
brew services start mysql<br>
brew services stop mysql<br>

- 일반모드
mysql.server.start<br>
mysql.server.stop<br>

### 실행 확인
brew services list

### 보안 적용
mysql_secure_installation <br>
비밀번호 세팅, yyyy

### mysql 실행
mysql -uroot -p비밀번호

### mysql 계정 생성
create user '유저명'@'localhost' identified by '비밀번호';

### mysql 계정 확인
SELECT user,authentication_string,plugin,host FROM mysql.user;

### mysql 계정 권한 적용
GRANT ALL PRIVILEGES ON *.* TO '유저명'@'localhost'; <br>
GRANT GRANT OPTION ON *.* TO '유저명'@'localhost'; <br>
flush privileges; // 실시간 반영

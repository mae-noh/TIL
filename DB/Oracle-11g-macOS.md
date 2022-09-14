# MacOS에서 Oracle 설정

docker 다운로드
brew install --cask docker

docker pull wnameless/oracle-xe-11g-r2

docker images

docker run --name oracle_db_11gr2 \
> -d \
> -p 51521:1521 \
> -p 55500:5500 \
> wnameless/oracle-xe-11g-r2

docker exec -it oracle_db_11gr2 bash
sqlplus system/oracle

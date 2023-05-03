# Apache Superset
```
- 데이터 시각화 및 비즈니스 인텔리전스(BI) 플랫폼
- 데이터 분석에 전문지식이 없어도 분석 작업을 할 수 있음
- Airflow를 만든 Airbnb에서 시작한 프로젝트
- python으로 개발
```

## Installing Superset Locally Using Docker Compose

### Docker Engine 및 Docker Compose 설치
https://docs.docker.com/desktop/install/mac-install/
<br><br>

### Superset's GitHub repository 복제
```
git clone https://github.com/apache/superset.git
```

### Docker Compose를 통해 Superset 실행
```
cd superset
```

```
docker-compose -f docker-compose-non-dev.yml pull
docker-compose -f docker-compose-non-dev.yml up
```

### Superset에 로그인
http://localhost:8080
```
username: admin
password: admin
```

<br>

## 환경 설정  
- 경로 `docker/pythonpath_dev/superset_config.py`<br>
  [ superset git 복제한 폴더 아래에 존재 ]
  - superset version 2.0.0으로 변경<br>
    ```
    x-superset-image: &superset-image apache/superset:${TAG:-latest-dev}
    x-superset-image: &superset-image apache/superset:2.0.0 # 변경
    ```
  
  - x-superset-volumes 이미지 확장 기능
    ```
    x-superset-volumes: &superset-volumes
    # /app/pythonpath_docker will be appended to the PYTHONPATH in the final container
      - ./docker:/app/docker
      - superset_home:/app/superset_home
    
    x-superset-volumes: &superset-volumes
    # /app/pythonpath_docker will be appended to the PYTHONPATH in the final container
      - ./docker:/app/docker
      - superset_home:/app/superset_home
      - 경로 추가
    ```

- 경로 `docker/.env-non-dev` 수정<br>
  superset 설치된 후, 자동으로 생성되는 샘플데이터와 샘플 대시보드를 사용하지 않음.<br>
  superset 인스턴스가 가벼워지며, 필요한 데이터와 대시보드만 추가하여 사용 가능.<br>
  ```
  SUPERSET_LOAD_EXAMPLES=no
  ```
    
- 대시보드 기능 활성화<b>
  경로 `docker/pythonpath_dev/superset_config.py`
  - 

## DB 연결하기

## Installing Superset from Scratch

### OS Dependencies
- 운영체제 버전 확인
  ```
  lsb_release -a
  ```
- required dependencies (Ubuntu 20.04)
  ```
  sudo apt-get install build-essential libssl-dev libffi-dev python3-dev python3-pip libsasl2-dev libldap2-dev default-libmysqlclient-dev
  ```

### Python Virtual Environment
- 파이썬 가상환경 설치
  ```
  python3 -m venv venv-superset
  . venv-superset/bin/activate
  ```

### Installing and Initializing Superset
- apache-superset
  ```
  pip install apache-superset
  ```
- 에러 발생
  ```
  Failed to build apache-superset cron-descriptor func-timeout pgsanity python-geohash wtforms-json pymeeus
  ```
- 해결 방법
  ```
  "error: invalid command 'bdist_wheel'"은 일반적으로 Python 패키지를 빌드할 때 발생하는 오류 중 하나입니다. 
  이 오류는 일반적으로 "wheel" 패키지가 설치되어 있지 않을 때 발생합니다. `pip install wheel`
  ```
  

### `python3 venv` vs `pyenv` 차이점
```
python3 venv는 Python 프로젝트마다 독립된 가상환경을 생성하고 관리할 수 있음.
pyenv는 시스템 전체에서 Python 버전을 관리하고 프로젝트별로 다른 Python 버전을 사용할 수 있음.
```

### 참고
- https://randalee.github.io/python/superset-test-01/
- [공식] https://superset.apache.org/docs/installation/installing-superset-from-scratch#os-dependencies

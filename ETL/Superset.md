# Apache Superset
```
- 데이터 시각화 및 비즈니스 인텔리전스(BI) 플랫폼
- 데이터 분석에 전문지식이 없어도 분석 작업을 할 수 있음
- Airflow를 만든 Airbnb에서 시작한 프로젝트
- python
```

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

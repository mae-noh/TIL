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
    
- 대시보드 기능 활성화<br>
  경로 `docker/pythonpath_dev/superset_config.py`
  
  ```
  APP_NAME = "etoos_Superset"
  
  FEATURE_FLAGS = {
    "ALERT_REPORTS": True,
    "DASHBOARD_RBAC": True,
    "DISABLE_SEGACY_DATASOURCE_EDITOR": False,
    "DASHBOARD_NATIVE_FILTERS": True,
    "DASHBOARD_CROSS_FILTERS": True,
    "DASHBOARD_NATIVE_FILTERS_SET": True,
    "ENABLE_TEMPLATE_PROCESSING": True,
    "ESCAPE_MARKDOWN_HTML": False
  }
  ```
  - "ALERT_REPORTS": True<br>
    대시보드에서 경고 및 보고서를 활성화합니다. 이 기능을 사용하면 데이터에 대한 경고를 생성하고 이메일, Slack 등으로 경고를 전송할 수 있습니다.
  - "DASHBOARD_RBAC": True<br>
    대시보드 역할 기반 접근 제어 (RBAC)을 활성화합니다. 이 설정을 사용하면 대시보드에 대한 액세스 권한을 부여할 수 있는 역할을 생성할 수 있습니다.
  - "ENABLE_TEMPLATE_PROCESSING": True<br>
    대시보드에서 Jinja 템플릿을 사용하여 데이터를 처리하고 처리된 결과를 표시하는 기능을 활성화합니다.
  - "ENABLE_TEMPLATE_REMOVE_FILTERS": True<br>
    대시보드에서 Jinja 템플릿을 사용할 때, 템플릿에서 필터를 제거하는 기능을 활성화합니다. 이 기능을 사용하면 대시보드에서 필터를 무시하고 템플릿에 하드 코딩된 데이터를 표시할 수 있습니다.
  - "ESCAPE_MARKDOWN_HTML": False<br>
    대시보드에서 Markdown 텍스트를 사용할 때, HTML 특수 문자를 이스케이핑하지 않도록 설정합니다. 이 설정을 사용하면 HTML 코드를 포함한 Markdown 텍스트를 대시보드에서 표시할 수 있습니다.
  - "DASHBOARD_NATIVE_FILTERS": True<br>
    대시보드에서 네이티브 필터를 사용하는 기능을 활성화합니다. 이 설정을 사용하면 대시보드에서 데이터를 필터링할 수 있는 인터페이스를 제공합니다.
  - "DASHBOARD_CROSS_FILTERS": True<br>
    대시보드에서 크로스 필터 기능을 활성화합니다. 이 설정을 사용하면 하나의 대시보드에서 선택된 값에 대한 필터링이 다른 대시보드에도 적용됩니다.
  - "DASHBOARD_NATIVE_FILTERS_SET": True<br>
    대시보드에서 네이티브 필터 설정을 활성화합니다. 이 설정을 사용하면 필터 설정을 저장하여 나중에 다시 사용할 수 있습니다.

## DB 연결하기

### DB 종속성 추가
https://superset.apache.org/docs/databases/docker-add-drivers/
```
touch /docker/requirements-local.txt
vi /docker/requirements-local.txt
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

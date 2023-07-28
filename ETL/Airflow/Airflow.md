# Airflow

## DAG (Directed Acyclic Graph)
DAG는 Airflow에서 작업을 조직화하고, 예약된 작업의 스케줄링을 관리하기 위한 그래프 구조. <br>
방향성이 있는 비순환 그래프. <br>
방향을 가지지만 루프가 존재하지 않는 그래프. <br>
자기 자신에서 출발해서 자기 자신으로 도착하면 순환, 루프가 존재한다고 말한다. <br>
이러한 경로가 없는 것이 비순환 그래프.

## Task
Task는 DAG의 작업 단위. <br>
각 Task는 DAG 내에 정의되며, Task의 실행 단위가 됩니다.

## Install
M1을 이용하여 Airflow 설치시 가상환경 필요.

- 변수 설정
  ```
  export AIRFLOW_HOME = '경로'
  echo $AIRFLOW_HOME
  ```

- 가상환경 설정
  ```
  # 가상환경 생성
  $ python3 -m venv venv-airflow

  # 가상환경 실행
  $ source venv-airflow/bin/activate
  ```

- docker-compose.yaml 파일 다운
  ```
  curl -LfO 'https://airflow.apache.org/docs/apache-airflow/{원하는 버전}/docker-compose.yaml'

  # 예
  curl -LfO https://airflow.apache.org/docs/apache-airflow/2.3.3/docker-compose.yaml
  ```

- `.env` 파일
  ```
  # 확인
  echo $(id -u) # ex) 1001

  # 파일생성
  vi .env

  ######################
  AIRFLOW_UID=1001
  ######################
  ```

- requirements.txt 파일 생성
  ```
  --constraint "https://raw.githubusercontent.com/apache/airflow/constraints-2.3.0/constraints-3.7.txt"
  boto3==1.22.0
  elasticsearch==7.13.4
  fsspec==2022.3.0
  s3fs==0.4.2
  apache-airflow-providers-microsoft-mssql==2.1.3
  apache-airflow-providers-odbc==2.0.4
  pymssql==2.2.5
  mysql-connector-python==8.0.29
  mysqlclient==2.1.0
  apache-airflow-providers-mysql==2.2.3
  apache-airflow-providers-elasticsearch==3.0.3
  opensearch-py==2.1.1
  ```

- Dockerfile 파일 생성
  ```
  FROM apache/airflow:2.3.3
  COPY requirements.txt .
  RUN pip3 install --upgrade pip
  RUN pip3 install awscli
  RUN pip3 install -r requirements.txt
  ```

- 도커 실행
  ```
  docker-compose up
  ```

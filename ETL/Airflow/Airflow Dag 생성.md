# Airflow Dag 생성

## 기본 Dag 생성
`/Airflow/dags` 폴더 내에 python 파일 생성<br>
파일 내에 아래 코드 작성 후 저장, 조금 기다리면 Airflow에 뜨는것 확인 가능.

```
from airflow import DAG
from datetime import datetime

default_args = {
    'start_date': datetime(2023, 6, 5)
}
with DAG(dag_id='my_first_dag', schedule_interval='@daily', default_args=default_args) as dag:
    task1 = DummyOperator(task_id='task1')
    task2 = DummyOperator(task_id='task2')
    task3 = DummyOperator(task_id='task3')
    
    task1 >> task2 >> task3
```
- `start_date` 시작 날짜
- `dag_id` DAG 이름
- DAG은 `task`단위로 이루어져 있다
- `Connections` 연결 정보를 Airflow에 정의하여 사용 가능
- `XComs` 리턴값을 저장하여 꺼내 쓸 수 있음

## ES 인덱스 Dag 생성
```
from datetime import datetime
from airflow import DAG
from airflow.operators.python_operator import PythonOperator
from elasticsearch import Elasticsearch

default_args = {
    'owner': 'airflow',
    'schedule_interval': '@daily',
    'start_date': datetime(2023, 6, 6),
    'tags': ['temp']
}

dag = DAG(
        dag_id='test_dag',
        default_args=default_args,
        catchup=False
)

def connect_to_opensearch():
    es = Elasticsearch(
            hosts='host',
            http_auth=("username", "password")
    )

    print(es.info())

connect_task = PythonOperator(
    task_id='connect_to_opensearch',
    python_callable=connect_to_opensearch,
    dag=dag
)
```

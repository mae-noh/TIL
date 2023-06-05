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
- start_date : 시작 날짜
- dag_id : Dag 이름

## ES 인덱스 Dag 생성


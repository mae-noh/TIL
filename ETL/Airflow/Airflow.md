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

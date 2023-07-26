# Airflow 재수행 방법

## DAG 단위로 재수행
<img width="1191" alt="image" src="https://github.com/mae-noh/TIL/assets/65100355/871e18c3-3f2a-45d0-9701-2273bff289ef">
  
  - Trigger DAG
  - Trigger DAG w/ config


## TASK 단위로 재수행
<img width="479" alt="스크린샷 2023-07-26 오후 2 24 51" src="https://github.com/mae-noh/TIL/assets/65100355/b6bd5052-0b32-4308-a60f-516a2f7461c5">
  
  - Run
    - Ignore All Deps
    - Ignore Task State
    - Ignore Task Deps
 
  - Clear
    - Past
      해당 TASK의 과거 시점 TASK들을 같이 삭제한다.
    - Future
      해당 TASK의 미래 시점 TASK들을 같이 삭제한다.
    - Upstream
      해당 TASK의 의존성 상위 TASK들을 같이 삭제한다.
    - Recursive
      부모 DAG, 자식 DAG의 TASK들을 같이 삭제한다. (Sub DAG을 사용한 경우)
    - Failed
      실패한 TASK만 삭제한다

  * Past, Faield 옵션을 선택시, 과거 실패했던 TASK들을 삭제한다.
  
- Mark Failed
  
- Mark Success


## Backfill 재수행
수행되지 않은 기간의 DAG run을 수행

# Index Lifecycle Management - ILM 기능으로 인덱스 주기 관리하기.

- Index Management > Index Templates 생성
  - Logistics<br>
    ```
    Name:tomcat-monitoring-template // 템플릿명
    Index pattern:tomcat-monitoring-* // 인덱스 패턴과 일치시 적용할 예정
    ```

  - Settings<br>
    ```
    "number_of_shards": 4,
    "number_of_replicas": 1,
    "index.lifecycle.name": "tomcat-monitoring-ilm", // ILM명
    "index.lifecycle.rollover_alias": "tomcat-monitoring" // alias명
    ```
- Index Lifecycle Polices 생성<br>
  - `Name`: "tomcat-monitoring-ilm" // ILM명
  - Hot phase,  Rollover 설정 <img width="2720" alt="스크린샷 2022-12-01 오후 2 38 48" src="https://user-images.githubusercontent.com/65100355/204974418-cb42c4e2-0c61-49e8-b6bf-7d93a4d2b5af.png">
    - Maximum age :  
    - Maximum documnets : 문서수가 N개 이상일 경우 Rollover Start
  - Warm phase
    - Shrink : shards 개수 조정
    - Force merge : segment 개수 조정
  - Cold phase
    - Searchable snapshot : 실제 사용하던 replica들이 스냅샷으로 저장됨
  - Delete phase

- 인덱스 alias 지정하여 생성
  ```
  PUT tomcat-monitoring-2022-12
  {
    "aliases" : {
      "my-index" : {
        "is_write_index": true
      }
    }
  }
  ```
  
- 인덱스 alias 추가
  ```
  POST /_aliases?pretty
  {
    "actions": [
      {
        "add": {
          "index": "tomcat-monitoring-2023-01",
          "alias": "monitoring",
          "is_write_index": true
        }
      }
    ]
  }
  ```
 
- ES 확인 명령어
  ```
  GET _cat/nodes // WARM, HOT, COLD 확인 가능
  GET _cat/shards/*tomcat-monitoring* // Primary, Shard 확인 가능
  GET tomcat-monitoring-2022-10/_alias
  ```
- lifecycle 테스트 확인을 위해 refresh 주기 변경
  ```
  #default 10m
  PUT _cluster/settings
  {
    "transient": {
      "indices.lifecycle.poll_interval": "5s"
    }
  }
  ```
  
- ilm 조회
  ```
    GET _ilm/policy/monitoring-ilm
  ```

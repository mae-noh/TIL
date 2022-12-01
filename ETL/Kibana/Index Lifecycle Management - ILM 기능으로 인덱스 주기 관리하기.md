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
    "index.lifecycle.name": "tomcat-monitoring-ilm" // ILM명
    "index.lifecycle.rollover_alias": "tomcat-monitoring" // alias명
    ```
- Index Lifecycle Polices 생성<br>
  - ```Name: "tomcat-monitoring-ilm" // ILM명```
  - ```Hot phrase,  Rollover 설정``` <img width="2720" alt="스크린샷 2022-12-01 오후 2 38 48" src="https://user-images.githubusercontent.com/65100355/204974418-cb42c4e2-0c61-49e8-b6bf-7d93a4d2b5af.png">

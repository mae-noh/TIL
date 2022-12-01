# Index Lifecycle Management - ILM 기능으로 인덱스 주기 관리하기.

- Index Management > Index Templates 생성
  - Logistics<br>
  `Name`:tomcat-monitoring-template // 템플릿명<br>
  `Index pattern`:tomcat-monitoring-* // 인덱스 패턴과 일치시 적용할 예정<br>

  - Settings<br>
    ```
    "number_of_shards": 4,
    "number_of_replicas": 1,
    "index.lifecycle.name": "tomcat-monitoring-ilm" // ILM명
    "index.lifecycle.rollover_alias": "tomcat-monitoring" // alias명
    ```

- Index Lifecycle Polices 생성

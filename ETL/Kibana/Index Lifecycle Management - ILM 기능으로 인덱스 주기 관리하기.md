# Index Lifecycle Management - ILM 기능으로 인덱스 주기 관리하기.

```
기존 인덱스에 적용하는 경우를 살펴보겠습니다.
순서는 다음과 같습니다.

1. Index Lifecycle Policies 생성

2. Index Template 생성 및 수정
  - Setting에 [ILM명], [rollover_alias] 추가

3. 기존 인덱스 reindex
  - 인덱스명 패턴 주의 (정규식패턴 '^.*-\d+$'과 일치하도록)
  - 인덱스 템플릿이 적용되었는지 확인

4. 인덱스 alias, 옵션값 is_write_index: true 추가
  - 2번에 [rollover_alias] 설정한값과 동일하게 [alias] 추가

5. 데이터 색인 및 추가시 인덱스명이 아닌 alias명으로 실행
```

<br>
<br>
<br>

## 1. Index Lifecycle Policies 생성.
![image](https://user-images.githubusercontent.com/65100355/212607021-7a7dc12c-87b7-464e-9915-9cdea29b6a25.png)
  ### ILM명 정의
  ```
  name : "monitoring-ilm"
  ```
  ### ILM 정책(Hot, Warm, Cold, Delete)
  ```
  💡 인덱스를 주기적으로 rollover 및 삭제 가능
  ```
  <img width="552" alt="image" src="https://user-images.githubusercontent.com/65100355/212612991-81e6bb25-c395-405a-9c7d-a18475af4ead.png">
    
  ### Hot
  > Hot으로 설정된 인덱스의 경우, 다른 인덱스보다 먼저 복구되도록 우선순위가 높은 값으로 설정.<br>
  > 현재 인덱스가 특정 크기(shard size, index size), 문서 수(documents) 또는 수명(age)에 <b>도달</b>하면 새 인덱스에 쓰기 시작.<br>
  > OR 조건, 조건 중 하나라도 만족하면 rolling 시작.
  <img width="1089" alt="image" src="https://user-images.githubusercontent.com/65100355/212608138-029067da-0560-48ea-9203-c2739a18e933.png">

  ### Warm
  > 인덱스가 Warm 단계로 진입시, 샤드 수 축소, 세그먼트 병합 가능.<br>
  > 인덱스 우선순위를 Hot보다 낮게 설정.<br>
  - Replicas : replica 개수 조정
  - Shrink : shards 개수 조정
  - Force merge : segment 개수 조정
  
  ### Cold
  > Hot, Warm보다 낮은 우선순위. 만약의 경우를 대비하여 유지하는 경우.
  - Searchable snapshot : 실제 사용하던 replica들이 스냅샷으로 저장됨
   
  ### Delete
  > 인덱스 삭제, min_age 지정 필요.

<br>
<br>
<br>

## 2. Index Templates 생성
### Index Management > Index Template 
  - Logistics<br>
    ```
    Name:tomcat-monitoring-template // 인덱스 템플릿명
    Index pattern:tomcat-monitoring-* // 인덱스 패턴과 일치시 적용할 예정
    ```

  - Settings<br>
    ```
    "number_of_shards": 4,
    "number_of_replicas": 1,
    "index.lifecycle.name": "tomcat-monitoring-ilm", // ILM명
    "index.lifecycle.rollover_alias": "tomcat-monitoring" // alias명
    ```

<br>
<br>
<br>

## 3. Index에 alias 지정
### 인덱스명
```
💡index name does not match pattern '^.*-\d+$'
```
- 인덱스명의 경우 정규식 패턴 '^.*-\d+$'과 일치해야함
  `index-01`
  
### reindex
   ```
   POST _reindex?wait_for_completion=false
   {
     "source": {
       "index": "기존인덱스명"
     },
     "dest": {
       "index": "새인덱스명"
     }
   }
   ```

### 새 인덱스 alias 지정하여 생성시
  ```
  PUT tomcat-monitoring-2022-12
  {
    "aliases" : {
      "tomcat-monitoring" : {
        "is_write_index": true
      }
    }
  }
  ```
  
### 기존 인덱스에 alias 추가시
  ```
  POST /_aliases?pretty
  {
    "actions": [
      {
        "add": {
          "index": "tomcat-monitoring-2023-01",
          "alias": "tomcat-monitoring",
          "is_write_index": true
        }
      }
    ]
  }
  ```

### lifecycle 테스트 확인을 위해 refresh 주기 변경
  ```
  #default 10m
  PUT _cluster/settings
  {
    "transient": {
      "indices.lifecycle.poll_interval": "5s"
    }
  }
  ```

### ES 명령어
  ```
  GET _cat/nodes // WARM, HOT, COLD 확인 가능
  GET _cat/shards/*tomcat-monitoring* // Primary, Shard 확인 가능
  GET tomcat-monitoring/_ilm/explain
  GET _ilm/policy/monitoring-ilm
  ```


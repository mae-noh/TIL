## OpenSearch DBAPI

> OpenSearch에는 기존 Elasticsearch에서 제공되던게 안되는게 너무 많다..<br>
> Superset에서 커넥션 연결 템플릿은 공식문서에도 안적혀있고 github에서 겨우 찾음<br>
> 당연히 alias로도 검색해서 가져올 줄 알았는데.. 왜 안되니..<br>

#### 해결 방법
- sql 코드에 v2 버전이 있길래 뭔가했는데,, 추가 기능을 제공하는 버전인가봄.
- sql engine v2는 기본적으로 비활성화되어있고
- DB 연결시 파라미터에 추가시  `/?v2=true`를 추가해줘야함
- github README를 차근차근 놓치지 말고 읽자 :)
- 참고 : https://github.com/opendistro-for-elasticsearch/sql/blob/develop/docs/dev/NewSQLEngine.md

## Superset 버전 변경
경로 > `docker/pythonpath_dev/superset_config.py`

- DB 업그레이드 `SECRET_KEY` 설정 필요  
  참고 [https://superset.apache.org/docs/installation/configuring-superset/#adding-an-initial-secret_key]
  1. `superset_config.py`에 `SECRET_KEY` 다음 암호화 값을 생성하여 `openssl rand -base64 42` 추가
  2. docker superset 컨테이너 명령어를 실행하기 위해 `docker exec -it superset_app /bin/bash`
  3. superset re-encrypt-secrets 실행시 적용 완료
  
- 원하는 버전으로 변경시, 데이터 그대로 docker image 변경
  ```
  x-superset-image: &superset-image apache/superset:${TAG:-latest-dev}
  x-superset-image: &superset-image apache/superset:2.0.0 # 변경
  ```

## CUSTOM TIME COLUMN 추가
- `CUSTOM_SQL`에 추가, 기존 컬럼을 기준으로 새로운 컬럼 생성  
`CONVERT_TZ(DATE_FORMAT(server_time, '%Y-%m-%d %H:%i:%s'), 'UTC', 'Asia/Kolkata')`

## TIME GRAIN
> TIME GRAIN에 `Week` 없음..
> config파일에 추가해주면 될것 같은데 안나옴..

## Connection 연결시 비밀번호 인코딩 에러
```
SQLALCHEMY_DATABASE_URI = "%s://%s:%s@%s:%s/%s" % (
  DATABASE_DIALECT,
  DATABASE_USER,
  DATABASE_PASSWORD,
  DATABASE_HOST,
  DATABASE_PORT,
  DATABASE_DB,
)
```

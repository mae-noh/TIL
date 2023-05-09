# AWS Lambda
```
- 서버리스, 함수, 애플리케이션 빌드 실행
- Rest API와 같은 HTTP 요청을 통해 함수를 호출, 리턴, 이벤트 발생
- 예를 들어, 데이터베이스의 읽기/쓰기 등을 위한 함수 구문을 클라우드에 업로드해둔다면
  어느 프로그램에서도 단순히 함수 호출을 통해 데이터베이스로부터 입출력이 가능
- 프로그래밍 로직에만 집중할 수 있도록 하는 것
- 프로젝트를 여러개의 함수로 쪼개고, 함수들이 실행되는 횟수만큼 비용을 내는 방식
```

- 장점
  ```
  실제 사용량에 대해서만 비용이 청구되므로 경제적
  성능,보안 관리 AWS가 관리하므로 운영관리에 대한 부담이 줄어듬
  ```

## OpenSearch?
```
아마존에서 지원하는 엘라스틱서치
```

### OpenSearch를 Lambda에서 이용한다?
```
1. AWS Lambda 함수에서 사용 가능한 OpenSearch 클라이언트 라이브러리를 설치
2. Lambda 함수에서 OpenSearch API를 이용하여 OpenSearch 클러스터와 통신
3. Lambda 함수에서 OpenSearch 클러스터 엔드포인트 URL, 인증 자격 증명을 설정
4. OpenSearch 클러스터 데이터를 색인하고 검색할 수 있음
```

## AWS Lambda에서 OpenSearch API를 사용하기!
- AWS Lambda 실행 예제<br>
https://aws.amazon.com/ko/getting-started/hands-on/run-serverless-code/

- Opensearch cluster 구축 해보기
  
- AWS Lambda에서 Opensearch API를 사용하는 예제
  ```
  import boto3
  from opensearchpy from OpenSearch

  def lambda_handler(event, context):
      # Opensearch 클러스터의 엔드포인트 URL과 인증 자격 증명 설정
      opensearch_host = ''
      opensearch_region = ''
      access_key = ''
      secret_key = ''

      # Opensearch 클러스터와 연결
      opensearch = OpenSearch(
          opensearch_host,
          http_auth = (access_key, secret_key),
          use_ssl = True,
          verify_certs=True,
          connection_class=RequestsHttpConnection
      )

      # Opensearch API 호출
      response = opensearch.search(
          index = 'your-index-name',
          body = {
              'query': {
                  'match': {
                      'your-field-name': 'your-search-keyword'
                  }
              }
          }
      )

      # Opensearch API 응답 처리
      results = response['hits']['hits']
      for result in results:
          print(result['_source'])
  ```
  
## 이벤트 발생시 API를 이용하여 OpenSearch에 데이터를 수집해보자.


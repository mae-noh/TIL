# AWS Lambda
```
- 서버리스 컴퓨팅 FaaS(Function as a Service)
- 개발자가 서버를 관리할 필요없이 애플리케이션을 빌드를 실행
- Rest API와 같은 HTTP 요청을 통해 함수를 호출, 리턴, 이벤트 발생
- 예를 들어, 데이터베이스의 읽기/쓰기 등을 위한 함수 구문을 클라우드에 업로드해둔다면
  어느 프로그램에서도 단순히 함수 호출을 통해 데이터베이스로부터 입출력이 가능
- 프로그래밍 로직에만 집중할 수 있도록 하는 것
- 프로젝트를 여러개의 함수로 쪼개고, 함수들이 실행되는 횟수만큼 비용을 내는 방식
```

- 장점
  ```
  - 실제 사용량에 대해서만 비용이 청구되므로 경제적
  - 성능,보안 관리 AWS가 관리하므로 운영관리에 대한 부담이 줄어듬
  ```

## OpenSearch?
```
아마존에서 지원하는 엘라스틱서치를 OpenSearch라고 부름
RDBMS 환경에서 ES를 사용하려면, RDBS를 Document형 DB로 변환해주는 작업 필요한데,
이 작업은 ELK로 ES-Logstash(데이터변환)-Kibana(대시보드및모니터링)을 지원
하지만 ELK를 구축하지 않고도, 오픈서치를 이용하면 ES를 이용할 수 있음
```

## AWS Lambda를 이용하여 OpenSearch를 설치해보자.
- AWS Lambda 실행<br>
https://aws.amazon.com/ko/getting-started/hands-on/run-serverless-code/

## 이벤트 발생시 API를 이용하여 OpenSearch에 데이터를 수집해보자.

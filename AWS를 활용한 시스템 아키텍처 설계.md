
## 사전 미션
- 도커(docker)에 대해 설명해주세요
    - 리눅스 컨테이너 기술을 기반으로 한 가상화 기술 중 하나.
    - 호스트 운영 체제의 커널을 공유하면서 프로세스를 격리하는 방식.
- 도커(docker)를 활용하면 어떤 장점이 있나요?
    - 라이브러리, 시스템 도구, 코드, 런타임 등 소프트웨어를 실행하는 데 필요한 모든 것이 포함되기때문에 원하는 환경을 동일하고 신속하게 구축 가능.
    - 환경에 구애받지 않고 애플리케이션을 신속하게 배포 가능.
- 서버리스(serverless)에 대해 설명해주세요
    - 클라우드 컴퓨팅 모델 중 하나.
    - 개발자가 서버 인프라를 직접 관리하지 않고 애플리케이션 구축, 실행 가능.
    - 예를 들어 AWS Lambda, 함수 기반으로 애플리케이션을 작성.
- 서버리스(serverless)를 활용하면 어떤 장점이 있나요?
    - 비용적 장점, 사용한 리소스에 대해서만 요금 청구.
    - 애플리케이션 부하에 따른 자동 스케일링.
    - 운영 업무 간소화.
- 서비스를 배포한 경험에 대해 자유롭게 작성해주세요
    - -
- AWS를 비롯한 클라우드 서비스의 장점은 무엇인가요?
    - 리소스를 자유롭게 축소,확장 가능.
    - 다양한 개발 환경을 제공.
- AWS를 비롯한 클라우드 서비스를 사용하면서 궁금한점이 있다면 작성해주세요
- 지금 운영중인 서비스의 아키텍처에 대해 궁금한 점이 있다면 작성해주세요 (회사/개인프로젝트 관계없이)
시간이 된다면 챌린지 시간에 리뷰해드리겠습니다
- 운영 중인 서비스를 그림으로 표현할 수 있다면 파일을 업로드해주세요
리뷰를 원하시는 분들은 시각자료가 있다면 많은 도움이 됩니다

## 강연 스케줄
### **scaling을 고려한 아키텍처 설계**

**AWS EC2, AWS RDS, AWS ElasticCache, AWS ALB, AWS CloudFront, AWS DynamoDB, AWS Lambda**

- RDS를 활용한 데이터베이스 scaling
- ALB + EC2를 활용한 서버 scaling
- Serverless 활용 시 장단점

아하모먼트 나에게 맞는 회사를 선택하는 방법

### **SNS 뉴스피드 피드 서비스 설계**

**AWS SQS, AWS SNS, AWS Neptune, AWS Aurora, AWS ElasticCache, AWS CloudFront**

- Message Queue를 활용한 느슨한 결합이란?
- 서비스 운영 방식에 맞는 데이터 스키마 설계와 데이터베이스 선택
- 올바른 ElasticCache 활용법

아하모먼트 사수/시니어 없는 환경에서 성장하기

### **실시간 채팅 서비스 설계**

**WebSocket, Container Orchestration, AWS ECS, AWS EKS, AWS Fargate, AWS ECR**

- WebSocket과 HTTP 통신의 차이점
- 분산 데이터베이스 시스템에서 Unique ID를 사용하는 방법
- health check와 container orchestration

아하모먼트 매력적인 이력서 작성법

### **영상 스트리밍 서비스 설계**

**AWS CloudFront, AWS S3, DAG, Consistency**

- AWS CloudFront Edge Location을 활용한 영상 스트리밍
- 분할된 영상을 DAG를 활용하여 업로드하는 방법
- 동시에 업로드를 시도하는 경우 에러 핸들링

아하모먼트 현업에서 ChatGPT를 활용하는 방법

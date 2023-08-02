# Airflow CICD 설정
GitHub Repository 내 DAG 코드를 Docker 컨테이너 내의 Airflow DAGs 폴더로 동기화

## 환경
- local
- airflow docker
  
<br>

## jenkins 설치
  ```
  brew install jenkins
  ```

- jenkins 실행
  ```
  /opt/homebrew/opt/jenkins/bin/jenkins --httpListenAddress=127.0.0.1 --httpPort=8888
  ```

  - 비밀번호 서버에서 확인
  - Install Suggested Plugins

<br>

## jenkins pipeline 생성
- jenkins web
  ```
  localhost:8888
  ```
  
- 새로운 item 생성 선택
  ![image](https://github.com/mae-noh/TIL/assets/65100355/9c01272e-ef51-4723-b989-79bde1826634)

- pipeline 선택
  <img width="1478" alt="스크린샷 2023-08-02 오후 5 02 16" src="https://github.com/mae-noh/TIL/assets/65100355/9fca918c-ad32-4948-b100-13433b608577">

- configure 설정
  <img width="1482" alt="스크린샷 2023-08-02 오후 5 03 18" src="https://github.com/mae-noh/TIL/assets/65100355/fd5b2410-b3ff-42e7-b4bb-d7b96d5079ed">

  - GitHub project 옵션 선택 > Project url 입력
  - Github hook trigger for GITScm polling 옵션 선택
    Jenkins에서 GitHub 저장소와 연동하여 자동으로 빌드를 트리거하는 방법 중 하나.
    이 옵션을 선택하면 Jenkins가 GitHub 저장소의 이벤트를 수신하고, 저장소에 변경 사항이 발생할 때마다 Jenkins 작업을 자동으로 시작.
  - pipeline 작성
    ```
    pipeline {
      agent any
      stages {
          stage('Checkout') {
              steps {
                  git branch:'main', url: 'https://github.com/mae-noh/jenkins_airflow_cicd'
              }
          }
          stage('Sync to Airflow DAGs Folder') {
              steps {
                  sh 'docker cp $WORKSPACE/dags/ venv-airflow-airflow-webserver-1:/opt/airflow/'
              }
          }
       }
    }
    ```
    - agent any는 Jenkins 슬레이브를 사용하여 파이프라인을 실행하도록 지정하는 부분입니다. any는 사용 가능한 모든 노드에서 파이프라인을 실행할 수 있음을 의미합니다.
    - Checkout 스테이지
      https://github.com/mae-noh/jenkins_airflow_cicd에 있는 코드를 main 브랜치로부터 가져옵니다. git 커맨드를 사용하여 코드를 체크아웃합니다.
    - Sync to Airflow DAGs Folder 스테이지
      가져온 DAG 코드를 Airflow 컨테이너 내의 /opt/airflow/ 디렉토리로 동기화합니다.
      docker cp 명령어를 사용하여 호스트 머신의 dags/ 디렉토리에서 Airflow 컨테이너의 /opt/airflow/로 DAG 코드를 복사합니다.



## QnA
  - 서버가 다른 경우, docker에 어떻게 접근하는지?
  - git push가 일어나면 jenkins 작동하는지?

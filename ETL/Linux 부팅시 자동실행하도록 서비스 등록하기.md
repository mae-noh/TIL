# EC2 재부팅시 자동실행하도록 서비스 등록하기
> Superset, Airflow 모두 docker 기반으로 설치했음.

## Superset
```
sudo chkconfig docker on
```

## Airflow
- Airflow 스크립트 작성, DAG 및 작업들을 정의<br>
  현재는 웹 서비스만 띄워놓기때문에 생략.. 추후 DAG 만들면 같이 설정해줘야할듯<br>

- `/etc/systemd/system/` 디렉토리에 `airflow.service` 파일 저장<br>
  Airflow 스크립트를 실행하는 서비스로 등록<br>

  WorkingDirectory 경로에서 docker-compose up -d 실행

  ```
  [Unit]
  Description=Docker Compose Application Service
  Requires=docker.service
  After=docker.service

  [Service]
  Type=oneshot
  RemainAfterExit=yes
  WorkingDirectory=/home/plats/stack
  ExecStart=/usr/local/bin/docker-compose up -d
  ExecStop=/usr/local/bin/docker-compose down
  TimeoutStartSec=0

  [Install]
  WantedBy=multi-user.target
  ```

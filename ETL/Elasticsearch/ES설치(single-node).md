# ES 설치 (ver.2022.08)

## 환경
- LINUX
<br>

## 설치 패키지 다운로드
#### 최신 버전 다운로드 https://www.elastic.co/kr/downloads/elasticsearch
#### 모든 버전 다운로드 https://www.elastic.co/kr/downloads/past-releases#elasticsearch 

```
// 패키지 다운로드
curl -LO https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-{버전}-linux-x86_64.tar.gz

// 압축파일 풀기
tar -xzf elasticsearch-{버전}-linux-x86_64.tar.gz
```
<br>

## ES 실행
```
bin/elasticsearch
```
Elasticsearch 실행 시, 추가 옵션 사용 가능<br>
- `bin/elasticsearch -d` <br> 백그라운드 데몬 실행 옵션<br>
- `bin/elasticsearch -p <파일명>` <br> ES 프로세스 ID를 지정한 파일에 저장 <br> 실행 종료시, 파일은 자동으로 삭제됨<br>

- ES 실행시 에러 해결
  - `bootstrap check failure [1] of [1]: memory locking requested for elasticsearch process but memory is not locked`<br>
운영모드의 경우 Elasticsearch는 boostrap check 이라는 것을 통해 아래의 설정이 되어 있지 않으면 실행되지 않는다.<br>
Elasticsearch는 운영체제의 `Java VM 파일 오픈 개수`, `메모리 락`을 모두 제일 크게 활성화 해줘야 한다.<br>


    ```
    sudo vi /etc/security/limits.conf
    
    <계정명> hard memlock unlimited >> 하드 세팅으로 메모리 락 제한 없도록
    <계정명> soft memlock unlimited >> 소프트 세팅으로 메모리 락 제한 없도록
    <계정명> hard nofile 65536 >> 65536번의 파일을 열어 볼 수 있게 설정
    <계정명> soft nofile 65536 >> 65536번의 파일을 열어 볼 수 있게 설정
    <계정명> hard nproc 65536 >> 65536번의 프로시저를 실행 할 수 있게 설정
    <계정명> soft nproc 65536 >> 65536번의 프로시저를 실행 할 수 있게 설정
    ```
    ```
    sudo vi /etc/sysctl.conf

    vm.max_map_count=262144
    ```
  - `Permission denied`<br>
Elasticsearch 5.0 이후부터는 root에서 실행할 수 없도록 변경됨.<br>
계정 생성 후, 권한을 부여해야한다.
    ```
    // 디렉토리 권한 파악
    ls -l

    // 디렉토리 권한 <계정명>으로 변경하기, root계정으로 실행
    sudo chown -R <계정명>:<계정명> 디렉토리명
    
    // 다른 계정으로 로그인
    su <계정명>
    ```

## 환경 설정

- JAVA_HOME 설정
    ```
    vi bin/elasticsearch-env
    
    // 라인 번호 확인
    :set number
    
    // 39 ~ 41번째 라인 변경
    if [ ! -z "$ES_HOME" ]; then
      JAVA="$ES_HOME/jdk/bin/java"
      JAVA_TYPE="ES_HOME"
    
    ```

- Elasticsearch.yml

    ```
    cluster.name: kafka-test

    node.name: node-1

    path.data: /data/svc/stack/data/elasticsearch/node1-log-data

    path.logs: /data/svc/stack/data/elasticsearch/node1-log-logs

    bootstrap.memory_lock: true

    network.host: 0.0.0.0

    http.port: 9201

    discovery.seed_hosts: ["127.0.0.1"]

    cluster.initial_master_nodes: ["node-1"]
    ```


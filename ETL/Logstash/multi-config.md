# multi config 설정

### 주의사항
- pipeline명에는 하이픈(-)이 들어가면 안됨
- config마다 `beats { port => 5044 }` 들어있으면 안됨 <br>
  하나의 pipeline에서 5044로 받아준 후에 다른 pipeline으로 분기<br>

### config 설정
- /절대경로/logstash-7.17.1/config/test.conf
  ```
  input{
    pipeline {
      address => 'test'
    }

  }
  ```

- /절대경로/logstash-7.17.1/config/test-log.conf
  ```
  input{

    pipeline {
      address => 'testLog'
    }

  }
  ```

### pipeline.yml 설정

  ```
    - pipeline.id: beats-server
      queue.type: persisted
      config.string: |
              input { beats { port => 5044 } }
              output { pipeline { send_to => [ "test", "testLog"] } }
    - pipeline.id: test
      path.config: "/절대경로/logstash-7.17.1/config/test.conf"

    - pipeline.id: testLog
      path.config: "/절대경로/logstash-7.17.1/config/test-log.conf" 
  ```

# ISSUE
- config 설정 `들여쓰기` 중요* <br>
  에러는 안나는데 내가 원하는 형식으로 가져오지 않음.
  
- logstash 테스트 잠시 중단 후 재시작, 특정 날의 로그 가져오지 못함
  - 기존 .log파일만 수집 중
  - .log파일 백업 로테이션으로 .bk 파일(백업파일)로 변환되어 수집 대상에서 벗어남
  - .bk 확장자도 추가

- 압축파일(.zip) read
  ```
  input {
    exec {
      command => "unzip -q -c /절대경로/*.zip"
      interval => 10
    }
  }
  ```
- 파일 처음부터 읽기 옵션
    ```
    input {
      file {
       path=>"D:/TestFilePath/textlog.txt"
       start_position => "beginning"
       type => textfile
      }
    }
    ```
- 시간 UTC, KST**

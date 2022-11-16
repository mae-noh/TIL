- config 설정의 들여쓰기 중요.
- logstash 중단시 며칠의 로그를 가져오지 못하는 이슈
  - .log파일 로테이션 .bk 파일(백업파일)로 변환
  - 확장자 추가
- .zip 파일? logstash에서 zip 풀어서 읽을 수 있는지 확인
- 시간 UTC, KST
- file 처음부터 읽기 옵션
    ```
    input {
      file {
       path=>"D:/TestFilePath/textlog.txt"
       start_position => "beginning"
       type => textfile
      }
    }
    ```

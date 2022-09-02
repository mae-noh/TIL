# Logstash

- ETL 버전 통일
  Filebeat-Logstash-Elasticsearch

  https://www.elastic.co/kr/downloads/past-releases

  ![image](https://user-images.githubusercontent.com/65100355/186580490-bce108d1-35f8-479b-9d4d-356d7f4d0f19.png)

- 로그스태시 설치
  ```
  wget <링크주소복사>
  ```

- 로그스태시 conf 환경설정
  logsash-7.10.1/config/pipline.conf
  ```
  input{
    beats {
      port => 5044
    }
  }

  filter {
    grok {
      match => ["message", "(?<[iis][access][time]>(?<year>%{YEAR})-(?<month>%{MONTHNUM})-(?<day>%{MONTHDAY}) %{TIME:time}) %{NOTSPACE:[iis][access][site_name]} %{NOTSPACE:[iis][access][server_name]} %{IPORHOST:[destination][address]} %{WORD:[http][request][method]} %{URIPATH:[url][path]} %{NOTSPACE:[url][query]} %{NUMBER:[destination][port]:int} %{NOTSPACE:[user][name]} %{IPORHOST:[source][address]} HTTP/%{NUMBER:[http][version]} %{NOTSPACE:[user_agent][original]} %{NOTSPACE:[iis][access][cookie]} %{NOTSPACE:[http][request][referrer]} %{NOTSPACE:[destination][domain]} %{NUMBER:[http][response][status_code]:int} %{NUMBER:[iis][access][sub_status]:int} %{NUMBER:[iis][access][win32_status]:int} %{NUMBER:[http][response][body][bytes]:int} %{NUMBER:[http][request][body][bytes]:int} %{NUMBER:[temp][duration]:int} %{IPORHOST:[user][address]}"]
    }
    mutate {
      add_field => { "[index][time]" => "%{year}-%{month}"}
    }
    date {
      match => [ "[iis][access][time]", "ISO8601" ]
      remove_field => ["day","month","year","time"]
    }
  }

  output {
    stdout { }
    elasticsearch {
      hosts => ["<ES HOST>:<ES PORT>"]
      manage_template => true
      index => "%{[@metadata][beat]}-%{[@metadata][version]}-%{[tags][0]}-%{[index][time]}"
      // user => "<ID>"
      // password => "<PASSWORD>"
    }
  }
  ```

- 로그스태시 실행 -f 1개의 환경설정만 실행
  ```
   sudo bin/logstash -f config/beat-pipeline.conf
  ```
- logstash.yml 설정하여 복수의 환경설정 실행

  - logstash.yml
    ```
    config.reload.automatic: true
    config.reload.interval: 3s
    ```
  - pipeline.yml
    ```
    pipeline.id: <파이프라인명>
    path.config: "<CONFIG 설정파일 경로>"
    ```
  - logstash 실행
    ```
    bin/logstash
    ```

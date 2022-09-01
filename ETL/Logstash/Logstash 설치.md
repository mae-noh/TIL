# Logstash 설치

- ETL 버전 통일
  Filebeat-Logstash-Elasticsearch

https://www.elastic.co/kr/downloads/past-releases

![image](https://user-images.githubusercontent.com/65100355/186580490-bce108d1-35f8-479b-9d4d-356d7f4d0f19.png)

```
wget <링크주소복사>
```

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
  }
}
```

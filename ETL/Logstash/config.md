input{
  beats {
    port => 5044 #logstash 5044 포트로 데이터를 받음 
  }
}

filter{

  if "_grokparsefailure" in [tags] {
    drop {}
  }

  if [tags][0] == "tomcat" {

    grok {
      match => ["message", "\[(?<logAccessTime>(?<year>%{YEAR})-(?<month>%{MONTHNUM})-(?<day>%{MONTHDAY}) %{TIME:time})\] \[%{NOTSPACE:thread}\] ERROR\s+%{JAVACLASS:class} %{NUMBER:code} \| (?<logMessage>(?m:.*))"]
    }

    mutate{
      add_field => {
        "logLevel" => "ERROR"
        "yearMonth" => "%{year}-%{month}"
        "logDateTime" => "%{year}-%{month}-%{day}T%{time}Z"
      }
      remove_field => ["day","month","year","time","agent","host","cloud"]
    }

    # KST to UTC
    date {
      match => ["logAccessTime", "YYYY-MM-dd HH:mm:ss.SSS"]
      timezone => "Asia/Seoul"
      target => "logDateTimeUTC"
    }

  }

  if [tags][0] == "iis" {

    # 멀티 패턴 적용
    grok {
      match => {
        "message" => [
          "(?<logAccessTime>(?<year>%{YEAR})-(?<month>%{MONTHNUM})-(?<day>%{MONTHDAY}) %{TIME:time}) %{NOTSPACE:iisAccessSiteName} %{NOTSPACE:iisAccessServerName} %{IPORHOST:destinationAddress} %{WORD:httpRequestMethod} %{URIPATH:urlPath} %{NOTSPACE:urlQuery} %{NUMBER:destinationPort} %{NOTSPACE:userName} %{IPORHOST:sourceAddress} HTTP/%{NUMBER:httpVersion} %{NOTSPACE:userAgentOriginal} %{NOTSPACE:iisAccessCookie} %{NOTSPACE:httpRequestReferrer} %{NOTSPACE:destinationDomain} (?<httpResponseCode>(.|400|401|403|404|405|500|503|504|505)) %{NUMBER:iisAccessSubStatus} %{NUMBER:iisAccessWin32Status} %{NUMBER:httpResponseBodyBytes} %{NUMBER:httpRequestBodyBytes} %{NUMBER:tempDuration} %{IPORHOST:clientAddress}",
          "(?<logAccessTime>(?<year>%{YEAR})-(?<month>%{MONTHNUM})-(?<day>%{MONTHDAY}) %{TIME:time}) %{NOTSPACE:iisAccessSiteName} %{NOTSPACE:iisAccessServerName} %{IPORHOST:destinationAddress} %{WORD:httpRequestMethod} %{URIPATH:urlPath} %{NOTSPACE:urlQuery} %{NUMBER:destinationPort} %{NOTSPACE:userName} %{IPORHOST:sourceAddress} HTTP/%{NUMBER:httpVersion} %{NOTSPACE:userAgentOriginal} %{NOTSPACE:iisAccessCookie} %{NOTSPACE:httpRequestReferrer} %{NOTSPACE:destinationDomain} %{NOTSPACE:logLevel} %{NUMBER:iisAccessSubStatus} %{NUMBER:iisAccessWin32Status} %{NUMBER:httpResponseBodyBytes} %{NUMBER:httpRequestBodyBytes} %{NUMBER:tempDuration} %{IPORHOST:publicAddress}"
        ]
      }
    }

    mutate {
      add_field => {
        "yearMonth" => "%{year}-%{month}"
        "logDateTime" => "%{year}-%{month}-%{day}T%{time}Z"
      }
      remove_field => ["day","month","year","time","agent","host","cloud"]
    }

  }

}

output {

  #grok pattern 실패시 파일에 저장 
  #if "_grokparsefailure" in [tags] {
  #file { path => "<저장 path>/error_grokparsefalure_%{[tags][0]}.txt" }
  #stdout { codec => rubydebug }
  #}
  
  #grok pattern 성공시 
  if "_grokparsefailure" not in [tags] {
    elasticsearch {
      hosts => ["<ip:port>"]
      manage_template => true
      index => "%{[tags][0]}-monitoring-%{yearMonth}"
      user => "<ES 보안 설정 id>"
      password => "<ES 보안 설정 pwd>"
    }
  }
 
}

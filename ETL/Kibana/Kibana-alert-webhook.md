# Kibana Slack Webhook 연동


### 보안 설정(single-node) 및 API key 설정

- Set up minimal security
`elasticsearch.yml`
  ```
  xpack.security.enabled: true
  discovery.type: single-node
  xpack.security.authc.api_key.enabled: true
  ```

- ES 실행 후 비밀번호 설정
  ```
  bin/elasticsearch
  bin/elasticsearch-setup-passwords interactive
  ```
- kibana 환경설정에 ES 보안 설정 `kibana.yml`
  ```
  elasticsearch.username:"kibana_system" // kibana default 계정 
  ```
  ```
  bin/kibana-keystore create
  bin/kibana-keystore add elasticsearch.password // kibana 비밀번호 설정
  ```

- kibana 실행
  ```
  bin/kibana
  ```

### Configuring Slack Accounts
- ES에 `Webhook URL` 설정
  ```
  bin/elasticsearch-keystore add xpack.notification.slack.account.monitoring.secure_url
  ```

- Slack notification attributes
  ```
  xpack.notification.slack:
    account:
      monitoring:
        message_defaults:
          from: x-pack
          to: notifications
          icon: http://example.com/images/watcher-icon.jpg
          attachment:
            fallback: "X-Pack Notification"
            color: "#36a64f"
            title: "X-Pack Notification"
            title_link: "https://www.elastic.co/guide/en/x-pack/current/index.html"
            text: "One of your watches generated this notification."
            mrkdwn_in: "pretext, text"
  ```


### Watcher
`threshold alert`, `advanced watch` 생성 가능<br><br>

<b>advanced watch</b>
- watcher 생성

  ![image](https://user-images.githubusercontent.com/65100355/192204746-4412fb5a-0421-420a-aaf0-1c44ae12b218.png)

  - `trigger > schedule > interval` 주기 설정
  - `input > search > request > body > query` 쿼리 설정
  - `input > search > request > indices` 인덱스 패턴 설정 
  - `action` 조건이 일치하면 action 정보에 따라 alert 실행
    - `actios > notify-slack > slack > messsage > text` {{ctx.payload.hits.hits}}{{_source.class}
 

- watcher 생성 후 확인 
  ```
  GET _watcher/watch/{id}
  ```


### Connector
alert이 발생했을때 alert을 어디 시스템(슬랙, 인덱스, 로깅 등)으로 보낼 것인지 지정<br>

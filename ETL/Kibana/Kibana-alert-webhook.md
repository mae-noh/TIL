# Kibana Slack Webhook 연동


### 보안 설정(single-node) 및 API key 설정

- Set up minimal security
elasticsearch.yml
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
- kibana 환경설정에 ES 보안 설정
```
elasticsearch.username:"kibana_system"
```
```
bin/kibana-keystore create
bin/kibana-keystore add elasticsearch.password
```

- kibana 실행
```
bin/kibana
```

### Connector
alert이 발생했을때 alert을 어디 시스템으로 보낼 것인가 지정하는 것





```
GET _watcher/watch/{id}
```

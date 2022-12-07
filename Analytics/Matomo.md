# Matomo
하나 이상의 웹사이트에 대한 온라인 방문을 추적하고 분석<br>
예) Google 애널리틱스

- DataLayer, hashMemberNo 통합회원번호를 해싱한 값
  - DataLayer란? 웹사이트에서 태그관리자로 정보를 전달하기 위한 자바스크립트 개체
  - GTM에서 사용하는 DataLayer를 그대로 이용

- 스크립트 삽입 방법
  - GTM 다음에 삽입되어야함, GTM이 없는 경우 <header>의 마지막 부분에 위치
  - 도메인, 컨테이너 ID 수정
  
- 방문자 쿠키
  - _pk_id, 기본 13개월
  - /var/www/html/piwik/js/container_(컨테이너 id).js에서 참조 확인 가능
- 세션 쿠키
  - _pk_ses
  - matomo_log_visit 테이블
  
- 태그 관리
  - Site
    - 웹사이트>관리, ETM 구축 서버 IP 입력
  
  - Variable
    - Enable Link Tracking 체크
    - Enable Cross Domain Linking 체크
    - Domain, 멀티 도메인 설정 가능. GNB를 통한 페이지 이동시 config_id 유지.
    - dataLayer에서 받을 hashMemberNo값 설정
  
  - Tag
    - Tracking Type '이벤트' 값으로 통일
    - Event Category 태그를 식별하기 위한 이름
    - Event Action {{hashMemberNo}}
    - Event Name, json 값으로 구성, ES에 object형태로 색인하여 하위 필드를 구성하기 위해
      - 통합회원가입 페이지(vue.js)에 Event Name 설정시: {"cur":"{{HistoryHashNewUrl}}", "ref":"{{HistoryHashOldUrl}}", "event": "visit", "user-agent": "{{UserAgent}}"}
      - 이투스닷컴&링커&큐리&스카이탭 페이지에 Event Name 설정시: {"cur":"{{PageUrl}}", "ref":"{{Referrer}}", "event": "visit", "user-agent": "{{UserAgent}}"}
  
  - Trigger
    - 트리거 설정시, 트리거명은 태그 이름과 동일하게 맞춤
    - 통합회원가입 페이지를 제외한 페이지, 유형 Pageview 값으로 설정
    - 통합회원가입 페이지 유형 History Change로 등록
  
  
--- 
- 트리거, CSS 태그를 잡아서 실제로 클릭을 수집하기 위한 설정을 함. 태그명과 일치시킴.
<img width="1158" alt="스크린샷 2022-12-07 오후 5 42 00" src="https://user-images.githubusercontent.com/65100355/206130232-ad214b83-4674-4725-aee2-18d2ced244a3.png">

- (스크립트) hashMemberNo값 로딩
```
  _mtm.push({
    'event': 'EtmExecute'
  });
```
  
- (스크립트) hashMemberNo값 로딩- Vue.js
```
  _mtm.push({
    'event': 'EtmExecuteVue'
  });
```

- trigger EtmExecute, EtmExecuteVue 실행
<img width="1205" alt="스크린샷 2022-12-07 오후 5 46 09" src="https://user-images.githubusercontent.com/65100355/206131117-98d0c4bf-f057-434b-bc61-9c84779430b4.png">
<img width="1327" alt="스크린샷 2022-12-07 오후 5 46 59" src="https://user-images.githubusercontent.com/65100355/206131302-79f07577-99af-45a5-88f2-3bb5cf1a2bf3.png">
  
### 질문리스트
- Q. Ingest 파이프라인, id_action_url필드를 정제하는 파이프라인, 파이프라인 적용은 자동으로되는지?
- Q. Cerebro Template, config_id(Session으로 사용할 필드)와 hashMemberNo의 차이점?
- Q. id_visitor
- Q. dataLayer, hashMemberNo 설정하는 방법?
- Q. 쿠키, 세션쿠키 둘 다 사용?
- Q. GA 유저 구분 방법 예시 설명
- Q. 맞춤 스크립트, 예시를 보면 달라지는게 event명뿐인데 예시라서 그런가?
  예) _mtm.push({’event’: ‘’})
- Q. 포털 대상 서비스 ETM 스크립트 삽입 요청은 볼 수 없는 페이지
- Q. Variable? 
- Q. GNB? config_id?는 무엇을 의미하는지?
- Q. Tag > EventName, {{PageUrl}} 값? 이벤트 발생시 넘어 오는 값인가?

- java ver.<br>
https://github.com/matomo-org/matomo-java-tracker


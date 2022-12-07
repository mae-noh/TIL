# Matomo
하나 이상의 웹사이트에 대한 온라인 방문을 추적하고 분석<br>
예) Google 애널리틱스

- Data Layer, hashMemberNo로 구분
  - data layer 웹사이트에서 태그관리자로 정보를 전달하기 위한 자바스크립트 개체
  - GTM에서 사용하는 dataLayer를 그대로 이용

- 스크립트 삽입 방법
  - GTM 다음에 삽입, GTM이 없는 경우 <head>안 마지막 부분에 위치
  - 도메인, 컨테이너 ID 수정
  
- 방문자 쿠키
  - _pk_id, 기본 13개월
  - /var/www/html/piwik/js/container_(컨테이너 id).js에서 참조 확인 가능
- 세션 쿠키
  - _pk_ses, 
  - matomo_log_visit
  
- 태그 관리
  - Site
    - 웹사이트 > 관리, ETM 구축 서버 IP 입력
  
  - Variable
    - Enable Link Tracking 체크
    - Enable Cross Domain Linking 체크
    - Domain, 멀티 도메인 설정 가능. GNB를 통한 페이지 이동시 config_id 유지.
    - dataLayer에서 받을 hashMemberNo값 설정
  
  - Tag
    - Tracking Type '이벤트'값으로 통일
    - Event Category 태그를 식별하기 위한 이름
    - Event Action {{hashMemberNo}}
    - Event Name, json 값으로 구성, ES에 object형태로 색인하여 하위 필드를 구성하기 위해
      - 통합회원가입 페이지(vue.js)에 Event Name 설정시: {"cur":"{{HistoryHashNewUrl}}", "ref":"{{HistoryHashOldUrl}}", "event": "visit", "user-agent": "{{UserAgent}}"}
      - 이투스닷컴&링커&큐리&스카이탭 페이지에 Event Name 설정시: {"cur":"{{PageUrl}}", "ref":"{{Referrer}}", "event": "visit", "user-agent": "{{UserAgent}}"}
  
  - Trigger
    - 트리거 설정시, 트리거명은 태그 이름과 동일하게 맞춤
    - 통합회원가입 페이지를 제외한 페이지, 유형 Pageview 값으로 설정
    - 통합회원가입 페이지 유형 History Change로 등록
  
### 질문리스트
- Q. Ingest 파이프라인, id_action_url필드를 정제하는 파이프라인, 파이프라인 적용은 자동으로되는지?
- Q. Cerebro Template, config_id(Session으로 사용할 필드)와 hashMemberNo의 차이점?
- Q. id_visitor
- Q1. dataLayer, hashMemberNo 설정하는 방법?
- Q2. 쿠키, 세션쿠키 둘 다 사용?
- Q3. GA 유저 구분 방법 예시 설명
- Q4. 맞춤 스크립트, 예시를 보면 달라지는게 event명뿐인데 예시라서 그런가?
예) _mtm.push({’event’: ‘’})
- Q5. 포털 대상 서비스 ETM 스크립트 삽입 요청은 볼 수 없는 페이지
- Q6. Variable? 
- Q7. GNB? config_id?는 무엇을 의미하는지?
- Q8. Tag > EventName, {{PageUrl}} 값? 이벤트 발생시 넘어 오는 값인가?


- java ver.
https://github.com/matomo-org/matomo-java-tracker


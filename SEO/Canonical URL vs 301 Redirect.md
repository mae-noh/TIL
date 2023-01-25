# Canonical URL vs 301 Redirect

## Canonical URL 설정
- canonical 뜻, "정식"
- 하나의 페이지를 가리키는 여러가지 URL이 존재, 그 중 원본 URL을 알려주는 태그
- html 내 <head> 섹션에 추가
  ```
  <link rel="canonical" href="https://example.com"/>
  ```
- http 응답 헤더에 명시
  ```
  HTTP/1.1 200 OK
  Content-Type: application/pdf
  Link: https://example.com; rel="canonical"
  Content-Length: ...
  ```

## 301 Redirect
- 하나의 페이지(A)를 다른 페이지(B)로 영구이동
- 유저가 A페이지 URL을 입력시, 301리다이렉트 설정시 B로 자동으로 연결됨

## Canonical URL 설정 선택
- 중복 콘텐츠 패널티 방지 가능
- 파라미터 사용
- 유사페이지 중 핵심페이지만 색인되면 될 경우
- 여러 URL로 접근할 수 있으나 동일한 페이지일 경우

## 301 Redirect 설정 선택 
- 하나의 URL로 합쳐도 되는 경우
- URL이 변경된 경우
- 새로운 버전의 페이지가 생긴 경우
- 동일한 두페이지를 만들었을때 하나는 사용하지 않는 경우
  
## 참고
https://www.ascentkorea.com/canonical-url-vs-301-redirect/

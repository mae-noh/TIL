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

## 
## 참고
https://www.ascentkorea.com/canonical-url-vs-301-redirect/

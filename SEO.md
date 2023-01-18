
# SEO (검색엔진최적화)

## Robots.txt
```
웹사이트 루트 디렉토리에 있는 텍스트파일
검색엔진 크롤러가 크롤링,색인 생성할 수 있는 페이지에 대한 지침을 제공
```

<br>

### Structure
  - User-agent : 어떤 검색엔진 크롤러를 지정할 것인가?
    - 구글: Googlebot
    - 네이버: Yeti
    - 다음: Daum
    - 빙: Bingbot
    - 덕덕고: DuckDuckBot
  - Disallow : 크롤링을 제한할 경로 (/ 상대경로)
  - Allow : 크롤링을 허용할 경로 (/ 상대경로)
  - Sitemap : 사이트맵이 위치한 경로의 전체 URL (https:// 부터 /sitemap.xml까지의 절대경로 URL)

```
* Robot.txt에서 특별하게 명시하지 않은 경우, 모두 크롤링 가능한것으로 간주됨
```

<br>

### Robot.txt 문법과 예시

#### Disallow
- 모든 또는 특정 크롤러의 특정 폴더 이하 제한 문법
  - 대상 : 모든 크롤러
  - 제한 디렉토리 : /do-not-crawl-this-folder/이하
    ```
    User-agent: *
    Disallow : /do-not-crawl-this-folder/
    ```
  - 대상 : 특정 크롤러
  - 제한 디렉토리 : /not-for-naver/이하
    ```
    User-agent: Yeti
    Disallow : /not-for-naver/
    ```
- 복수의 크롤러가 특정 디렉토리 이하 크롤링 제한 문법
  - 대상: 네이버 크롤러 (Yeti) & 덕덕고 크롤러 (DuckDuckBot) & 다음 크롤러(Daum)
  - 제한 디렉토리: /not-for-naver-and-duckduckgo-and-daum/ 이하
    ```
    User-agent: Yeti
    User-agent: DuckDuckBot
    User-agent: Daum
    Disallow: /not-for-naver-and-duckduckgo-and-daum/
    ```
- 복수의 크롤러를 제한하되, 제한하는 크롤러마다 다른 디렉토리를 차단하고 싶은 경우
  - 대상: 네이버 크롤러 (Yeti)
  - 제한 디렉토리: /not-for-naver/ 이하
  - 대상: 덕덕고 크롤러 (DuckDuckBot)
  - 제한 디렉토리: /not-for-duckduckgo/ 이하
    ```
    User-agent: Yeti
    Disallow: /not-for-naver/
  
    User-agent: DuckDuckBot
    Disallow: /not-for-duckduckgo/
    ```
  
- 복수의 크롤러 중 제한하는 크롤러를 묶어 각각 다른 디렉토리를 차단하고 싶은 경우
  - 대상: 네이버 크롤러 (Yeti) & 덕덕고 크롤러 (DuckDuckBot)
  - 제한 디렉토리 1: /not-for-naver-and-duckduckgo-1/ 이하
  - 제한 디렉토리 2: /not-for-naver-and-duckduckgo-2/ 이하
  - 제한 디렉토리 3: /not-for-naver-and-duckduckgo-3/ 이하
  - 대상: 다음 크롤러 (Daum)
  - 제한 디렉토리 1: /not-for-daum-1/ 이하
  - 제한 디렉토리 2: /not-for-daum-2/ 이하
    ```
    User-agent: Yeti
    User-agent: DuckDuckBot
    Disallow: /not-for-naver-and-duckduckgo-1/
    Disallow: /not-for-naver-and-duckduckgo-2/
    Disallow: /not-for-naver-and-duckduckgo-3/

    User-agent: Daum
    Disallow: /not-for-daum1/
    Disallow: /not-for-daum2/
    ```
  
<br>

#### Allow
```
Allow는 Disallow보다 우선권을 갖음
* 제한 디렉토리보다 상위 디렉토리를 허용하면 지정된 제한 디렉토리는 허용디렉토리와 상충되어 무효 처리됨
```

- 크롤링이 제한된 상위 서브폴더 이하의 디렉토리 중, 특정 세부 디렉토리를 따로 크롤링 허용하고 싶은 경우 사용
  - 대상: 네이버 크롤러 (Yeti)
  - 제한 디렉토리: /not-for-naver/ 이하
  - 허용 디렉토리: /not-for-naver/only-allow-here/ 이하
    ```
    User-agent: Yeti
    Disallow: /not-for-naver/
    Allow: /not-for-naver/only-allow-here/
    ```
 
<br>

### Sitemap
```
사이트맵 위치 명시, 복수의 사이트맵 위치 명시 가능
절대경로(전체 URL) 포함해야함
```

```
User-agent: *
Disallow: /do-not-crawl-here/
Sitemap: https://www.example.com/sitemap.xml
```

## Robot.txt 파일 업로드
- FTP를 이용하여 웹사이트 루트 디렉토리에 업로드

### 참고
- https://seo.tbwakorea.com/blog/robots-txt-complete-guide/

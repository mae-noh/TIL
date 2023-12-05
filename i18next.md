- 다국어 적용

- 한-영 번역 파일
    
    `static>locales>en`
    
    `static>locales>ko`

- init
```
const langDetectorOption = {
    order: ['querystring', 'cookie', 'navigator'],
    caches: ['cookie'],
    lookupQuerystring: "lang",
    cookieMinutes: 10, // 쿠키 만료 시간
    cookieDomain: Config[ENV].COOKIE_DOMAIN, // 쿠키 도메인
}
```

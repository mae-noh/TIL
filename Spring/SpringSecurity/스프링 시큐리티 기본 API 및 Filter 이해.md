# 인증 API

### 1. Form Login 인증

`http.formLogin`
```
http.formLogin()
    .loginPage("/login.html") // 사용자 정의 로그인 페이지
    .defaultSuccessUrl("/home") // 로그인 성공 후 이동 페이지
    .failureUrl("/login.html?error=true") // 로그인 실패 후 이동 페이지
    .usernameParameter("userId") // 아이디 파라미터명, default username
    .passwordParameter("passwd") // 패스워드 파라미터명, default password
    .loginProcessingUrl("/login_proc") // 로그인 Form Tag의 action url, default login 
    .successHandler(loginSuccessHandler()) // 로그인 성공 후 핸들러
    .failureHandler(loginFailureHandler()) // 로그인 실패 후 핸들러
```

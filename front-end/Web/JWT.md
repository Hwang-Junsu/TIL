# 기본 지식
## 1. JWT
Json Web Token의 약자로 모바일이나 웹의 사용자 인증을 위해 사용하는암호화된 토큰을 의미한다.
JWT 정보를 request에 담아 사용자의 정보 열람, 수정 등 개인적인 작업들을 수행할 수 있다.

## 2. XSS(Cross Site Scripting)
XSS라고 불리는 이유는 CSS가 이미 약자가 있기 때문이고
code injection attack이라고도 한다.

XSS도 다양한 공격 방법이 있는데 우선은
공격자가 의도하는 악의적인 js 코드를 피해자 웹 브라우저에서 실행시키는 것
정도로 알고 있으면 된다.

이 방법으로 피해자 브라우저에 저장된 중요 정보들을 탈취 가능하다.

## 3. CSRF(Cross Site Request Forgery)
정상적인 request를 가로채 피해자인 척 하고 백엔드 서버에
변조된 request를 보내 악의적인 동작을
수행하는 공격을 의미한다. (피해자 정보 수정, 정보 열람)

ex) 내가 쓰지 않은 광고성 글이 페이스 북에 올라갈 수 있음

대략적인 공격 과정은 다음과 같다. (요청 url은 알고 있다고 가정)
1. 공격자는 유저가 img를 열람하도록 하거나 link를 클릭하도록 유도한다.
2. 이 action은 사용자 의도와는 관계없이 http request를 보낸다.
3. 유저가 로그인이 되어있는 상태라면 이 request는 정상적으로 서버에 동작을 수행한다.

> ### 🙋‍♂️ XSS를 막으면 CSRF도 막히는 것 아닌가?   
>아니다. img 태그나 링크로도 사용자 브라우저에서
>악의적인 request를 보낼 수 있기 때문에   
>사용자 브라우저의 js를 조작하는 XSS와는 성격이 다르다.
 
또한 어려운 방법이지만 사용자 컴퓨터에 Web Proxy Tool을
설치할 수 있다면 request와 response를 탈취하고 조작할 수 있다.
이런 취약점을 막기 위해서는 서버 쪽에서
request의 조작 여부를 판단하도록 해야한다

4. XSS 공격을 막는 것은 웹 보안을 위한 최소한의 조치이다.
아무리 다른 공격(CSRF 등)에 대한 방비를 열심히 해도
XSS가 뚫린다면 아무 소용이 없다.

Js 코드로 의도하지 않은 request를 날린다던가
localStorage, 변수 값 등 모든 것이 탈취 가능하기 때문이다.

XSS 공격 방지는 웹 보안의 뿌리라고 할 수 있다.

### 🙄 JWT? 그냥 아무데나 저장하면 안돼?
1. JWT는 개인정보나 다름없다.
보안 관련 대책 없이 JWT를 아무 곳에나 저장을 한다는 것은
우리 고객 정보는 가져가도 상관없다는 의미나 다름 없다.

2. JWT를 private variable에만 저장하면 안될까?
UX 상 좋지 않다.

js variable은 웹페이지를 새로고침하면
사라지는 휘발성이다.

JWT를 private variable에 저장하는 것은 안되진 않지만
사용자 입장에서 화면을 새로고침할 때마다
새로 로그인을 해야한다면 어떨까?
매우 불편하고 귀찮을 것이다.
따라서 private variable에만 JWT를 저장하는 것은 피해야한다.

### 😵 그럼 어디에 저장할 수 있을까?
이제 JWT를 저장하기 위한 장소에는 2가지 정도가 남아 있다.
localStorage와 cookie.

먼저 결론부터 얘기하면 둘 중에 정답은 없다.
각각 장단점이 있고 개발 환경이 다르기 때문에
(서드파티 api를 사용해서 백엔드와 소통이 불가능하다던가...)
무엇이 더 우월하다는 이야기는 할 수 없다.

그럼에도 best option은 존재하니
궁금하신 분들은 결론을 봐주시길 바란다.

--- 
# 1. localStorage에 저장
👍 장점
CSRF 공격에는 안전하다.
그 이유는 자동으로 request에 담기는 쿠키와는 다르게
js 코드에 의해 헤더에 담기므로 XSS를 뚫지 않는 이상
공격자가 정상적인 사용자인 척 request를 보내기가 어렵다.

👎 단점
XSS에 취약하다.
공격자가 localStorage에 접근하는 Js 코드 한 줄만 주입하면
localStorage를 공격자가 내 집처럼 드나들 수 있다.

# 2. cookie에 저장
👍 장점
XSS 공격으로부터 localStorage에 비해 안전하다.

쿠키의 httpOnly 옵션을 사용하면 Js에서 쿠키에 접근 자체가 불가능하다.
그래서 XSS 공격으로 쿠키 정보를 탈취할 수 없다.
(httpOnly 옵션은 서버에서 설정할 수 있음)

하지만 XSS 공격으로부터 완전히 안전한 것은 아니다.
httpOnly 옵션으로 쿠키의 내용을 볼 수 없다 해도
js로 request를 보낼 수 있으므로 자동으로 request에 실리는 쿠키의 특성 상
사용자의 컴퓨터에서 요청을 위조할 수 있기 때문.
공격자가 귀찮을 뿐이지 XSS가 뚫린다면 httpOnly cookie도 안전하진 않다.

참고 : 'About XSS Attack' 부분 참고

👎 단점
CSRF 공격에 취약하다.
자동으로 http request에 담아서 보내기 때문에
공격자가 request url만 안다면
사용자가 관련 link를 클릭하도록 유도하여 request를 위조하기 쉽다.
참고 - 'Conclusion' 부분

(자동으로 request에 실리는 쿠키)

최근에는 쿠키의 CSRF 취약점을 막기 위해 쿠키의 same-site 속성과 js의 fetch api 속성의 기본값 등으로 request에 쿠키를 싣지 않음 이 설정되어있다.
쿠키가 request에 실리지 않는다면, 다음의 글을 보자

# 🎯 결론
1. best option
가장 좋은 방법으로는
refresh token을 사용하는 방법이 있다.

백엔드 api 개발자와 소통이 가능하다면
refresh token을 httpOnly 쿠키로 설정하고
url이 새로고침 될 때마다 refresh token을 request에 담아
새로운 accessToken을 발급 받는다.
발급 받은 accessToken은 js private variable에 저장한다.

이런 방식을 사용하는 경우,
refresh token이 CSRF에 의해 사용된다 하더라도
공격자는 accessToken을 알 수 없다.

CSRF는 피해자의 컴퓨터를 제어할 수 있는 것이 아니기 때문이다.
요청을 위조하여 피해자가 의도하지 않은
서버 동작을 일으키는 공격방법이기 때문에
refresh token을 통해 받아온 response(accessToken)는
공격자가 확인할 수 없다.

따라서 쿠키를 사용하여 XSS를 막고
refresh token 방식을 이용하여 CSRF를 막을 수 있다.

참고
프론트에서 안전하게 로그인 처리하기 (ft. React)
'store your refresh token in the cookie' 부분 참고

2. cookie와 localStorage, 굳이 1개를 택하라면?
반드시 cookie와 localStorage, 둘 중 하나를 선택하라고 한다면
나는 localStorage를 선호한다. 이유는 다음과 같다.

cookie의 httpOnly 옵션도 XSS 공격을 완벽히 막을 수 없다.
어차피 XSS 방어는 필수적이므로 cookie의 장점이
매력적이게 보이지 않는다.

cookie를 사용한다면 백엔드 api에 내가 사용하는 cookie를 위한
설정을 요구해야한다.
백엔드와 조율이 잘 되는 상태면 cookie를 사용해도 문제 없지만
서드파티 api의 경우 거의 불가능하므로 localStorage가 더 좋을 것 같다.

mdn은 저장소로 쿠키를 추천하지 않는다. 대신 ModernStorage(localStorage와 sessionStorage)를 추천한다.
참고 - mdn cookie

반대로, cookie를 지지하는 입장도 들어보자

🙋‍♂️ cookie를 지지하는 입장

CSRF 공격은 다루기 쉬운 반면 프론트엔드 크기가 크면 클수록
XSS 공격을 막기위한 작업은 많아지므로 쿠키 사용을 추천한다고 한다.
'Luc Engelen’s opinion' 부분 참고

+ 리뷰어님의 의견 (04-09 업데이트)

저는 cookie에 저장하는 편입니다. (가능하다면 httpOnly)
쿠키는 별도로 헤더에 담지 않아도 요청을 보낼때 자동으로 담아서 보내지기 때문에
매번 서버로의 요청에 담아야하는 토큰이라는 성격과 잘 맞고, 코드도 더 간결하게 작성할 수 있게 되는것같아요

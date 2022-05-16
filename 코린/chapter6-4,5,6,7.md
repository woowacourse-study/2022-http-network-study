
## 쿠키는 언제 사용할까?

**세션 관리(Session management)**

- 서버에 저장해야 할 로그인, 장바구니, 게임 스코어 등의 정보 관리

**개인화(Personalization)**

- 사용자 선호, 테마 등의 세팅

**트래킹(Tracking)**

- 사용자 행동을 기록하고 분석하는 용도

브라우저에 저장되기 때문에 민감한 정보는 저장하면 안된다.

## Set-Cookie (Response Header)


- Expires : 브라우저가 쿠키를 송출할 수 있는 유효기한을 지정
- Path : 쿠키 송출 범위를 특정 디렉토리에 한정
- Domain : 후방 일치가 된 도메인에 한정하여 쿠키를 송출.  Domain속성은 지정하지 않는 쪽이 안전.
- Secure : HTTPS에서 페이지가 열렸을 때만 쿠키 송출을 제한하기 위해 지정

위의 사진에서 sid는 sessionId이다.

로그인을 하지 않고 쿠팡에 접속해서 장바구니를 담았을 때, 해당 브라우저를 껐다가 켜도 내가 장바구니에 담았던 물품을 다시 확인할 수 있다. 서버는 비로그인 사용자를 sessionId로 판별한다.

사용자가 해당 세션 id로 페이지 이동을 할 때 마다 sid의 expires가 늘어난다. expires 내에 계속해서 서버에 요청을 보낸다면 오랫동안 세션을 유지할 수 있다는 의미이다.



### 브라우저에서 쿠키 확인


### **세션(HTTP Session) 절차**

1. 클라이언트가 서버에 Resource를 요청
2. 서버에서는 HTTP Request를 통해 쿠키에서 Session id를 확인을 한 후에 없으면 Set-Cookie를 통해 새로 발행한 `Session-id` 전송
3. 클라이언트는 HTTP Request 헤더의 Cookie필드에 Session id를 포함하여 원하는 Resource를 요청
4. 서버는 Session id를 통해 해당 세션을 찾아 클라이언트 상태 정보를 유지하며 적절한 응답

## Cookie (Request Header)


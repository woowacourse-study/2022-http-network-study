## Redirection 3XX

3xx 상태 코드는 User Agent 요청을 완료하기 위해 더 많은 액션을 취해야 함을 뜻한다. 

Location 헤더 필드가 제공되면 user agent 가 보통 자동으로 redirect 시킨다. 

### User Agent 란?

보통 브라우저를 말한다. 

기본 형태:

`User-Agent: <product> / <product-version> <comment>`

우리가 User Agent 를 볼 수 있는 곳!

주변을 잘 살피는 사려깊은 사람이라면 다 알만한!

#### Chrome
`user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/100.0.4896.127 Safari/537.36`

- Gecko: 렌더링 엔진

#### Safari
`user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/14.1.2 Safari/605.1.15`

#### Postman
`user-agent: PostmanRuntime/7.29.0`

#### curl
`user-agent: curl/7.64.1`

### 301 Moved Permanently

요청한 리소스의 주소가 영구적으로 바뀌었을 때 301 을 반환한다.

- http://leo0842.tistory.com 
    - 개발자 도구로 확인 가능하다.
- postman
  - 확인이 잘 안된다.
- curl -i http://leo0842.tistory.com
  - 헤더로 확인이 가능하다!

### 302 Found

요청한 리소스의 주소가 일시적으로 바뀌었을 때 302 를 반환한다.

#### TMI

- 원래는 Moved Temporarily 였다.

```java
  /**
    * {@code 302 Moved Temporarily}.
    * @see <a href="https://tools.ietf.org/html/rfc1945#section-9.3">HTTP/1.0, section 9.3</a>
    * @deprecated in favor of {@link #FOUND} which will be returned from {@code HttpStatus.valueOf(302)}
      */
//      @Deprecated
//      MOVED_TEMPORARILY(302, Series.REDIRECTION, "Moved Temporarily"),
```

언제 써봤을까요??

```
HTTP/1.1 302 Found
Keep-Alive: timeout=60
Connection: keep-alive
Content-Length: 0
Content-Language: ko-KR
Date: Mon, 02 May 2022 15:55:59 GMT
Location: http://localhost:8080/room/20
```

MVC 에서 return "redirect:" 사용 시 302를 반환하였다!

#### 301과 302의 차이점

- 301은 http -> https 와 같이 아예 안쓰는 주소로 리소스를 요청하여 영구적으로 바뀐 주소로 리다이렉트 시킬 때!
- 302는 redirect:/room/ + id 처럼 바뀔 가능성이 있는 주소로 리다이렉트 시킬 때!

### 303 See Other

클라이언트가 요청한 리소스를 다른 URI 에서 GET 요청을 통해 얻어야 할 때 사용하는 상태 코드

#### 301과 303의 차이점

- 301은 캐싱된 location 을 사용하여 돌려 보내준다!
- 303은 캐싱된 location 을 참조하지 않고 받은 location header 로 돌려 보내준다!

```java
class Test {
    
    @GetMapping("/test")
    public ResponseEntity<?> test() throws URISyntaxException {
        return ResponseEntity.status(HttpStatus.SEE_OTHER)
            .location(new URI("http://localhost:8080")).build();
    }
}
```

```java
class Test {
    
    @GetMapping("/test")
    public ResponseEntity<?> test() throws URISyntaxException {
        return ResponseEntity.status(HttpStatus.SEE_OTHER)
            .location(new URI("https://www.naver.com")).build();
    }
}
```

### 307 Temporary Redirect 과 308 Permanent Redirect

- 각각 302와 301과 매칭되는데 요청 메서드와 응답 바디가 변경되는 것을 금지

```java
class Test {

  @PostMapping("/test")
  public ResponseEntity<?> test() throws URISyntaxException {
    return ResponseEntity.status(HttpStatus.PERMANENT_REDIRECT)
            .location(new URI("http://localhost:8080")).build();
  }

  @PostMapping("/test2")
  public ResponseEntity<?> test2() throws URISyntaxException {
    return ResponseEntity.status(HttpStatus.MOVED_PERMANENTLY)
            .location(new URI("http://localhost:8080")).build();
  }
}
```

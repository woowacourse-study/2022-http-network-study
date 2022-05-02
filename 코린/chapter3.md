![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7d61453b-def9-433b-bf4d-30738268e352/Untitled.png)

# 4xx 에러

- **클라이언트 원인**으로 발생한 에러
- 서버에서 에러가 발생한 상황에 대한 설명과 이 에러가 일시적인지 영구적인지에 대한 설명을 entitty를 통해 반환해야 함.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d11a6b78-b818-4524-aa54-6d57c1ef8340/Untitled.png)

### 400 에러

- 잘못된 리퀘스트 구문의 반환 에러
- 브라우저는 200 OK와 동일하게 취급 (서버에서 에러를 처리했다는 뜻이므로)

```java
HttpStatus.BAD_REQUEST
```

### 401 에러

- 필요한 인증이 없는 경우
- 로그인을 하지 않은 채로 페이지 접근을 시도했을 때 반환

```java
HttpStatus.UNAUTHORIZED
```

### 403 에러

- 리소스에 접근 권한이 없는 경우
- 로그인 인증은 되었지만 접근 권한이 없는 무언가를 요청하는 경우에 반환

```java
HttpStatus.FORBIDDEN
```

### 404 에러

- 요청한 리소스가 서버에 존재하지 않거나 거부하는 이유가 분명한 경우

```java
HttpStatus.NOT_FOUND
```

# 5xx 에러

- **서버의 원인**으로 에러가 발생하고 있음을 나타냄
- 클라이언트의 요청에는 아무런 문제가 없으므로 수정 없이 다시 요청을 시도할 수 있음

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/63237942-33b5-43ac-a74b-176c729a064c/Untitled.png)

### 503 에러

- 사용자가 나중에 다시 시도해야 하는 경우 (서버가 과부화 상태이거나 점검중인 경우)

```java
HttpStatus.SERVICE_UNAVAILABLE
```

### 500 에러

- 코드가 잘못되었거나 요청을 처리하기 힘든 경우
- 런타임시에 발생하는 에러를 처리하지 못한 경우 발생

```java
HttpStatus.INTERNAL_SERVER_ERROR
```

# 4xx와 5xx의 차이

4xx는 클라이언트의 원인으로 발생, 5xx는 서버의 원인으로 발생

4xx의 경우 클라이언트가 원인을 해결하여 다시 요청을 보내야 하지만, 5xx는 클라이언트가 해결할 방법은 없다.

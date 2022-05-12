## Cache-Control 필드란?

- 캐싱 동작을 지정하는 HTTP 헤더의 필드
- 캐싱 동작을 지정하는 명령(필드값)을 디렉티브라고 칭함

- 디렉티브 표
|공통|Request 헤더|Response 헤더|
|------|---|---|
|no-cache|max-state|public|
|no-store|min-fresh|private|
|max-age||s-maxage|

## 디렉티브 종류

### max-age

`cache-control : max-age=[초]`

- Request 헤더에 쓰인 경우
    - 지정된 값보다 새로운 경우에는(?) 캐시되었던 리소스를 받아들임
    - max-age=0 이면 캐시 서버는 요청을 항상 오리진 서버에 넘김
- Response 헤더에 쓰인 경우
    - 캐시 서버가 유효성의 재확인을 하지 않고 리소스를 캐시에 보존해 두는 최대 시간을 나타냄

### s-maxage

`cache-control : s-maxage=[초]`

- 중간 캐시 서버에서만 적용되는 max-age 값을 설정하는 용도
- Cache-Control 값을 `s-maxage=31536000, max-age=0`
 과 같이 설정하면 캐시 서버에서는 1년동안 캐시되지만 브라우저에서는 매번 재검증 요청을 보내도록 설정됨

### no-cache

`cache-control : no-cache`

- Request 헤더에 쓰인 경우
    - 대부분의 브라우저에서 max-age=0 과 동일한 뜻을 가짐
    - Response에 대한 캐시는 저장하지만 사용하려고 할 때 마다 서버에 재검증 요청을 보냄
- Response 헤더에 쓰인 경우
    - 유효성 재확인 없이 캐시를 사용해서 안된다는 뜻을 가짐
    - 캐시 서버는 리소스를 저장할 수 없으며 이후의 요청에서 리소스의 유효성을 확인하지 않고는 캐시된 Response를 사용할 수 없게 됨
    - no-cache의 필드 값에 헤더 필드명이 지정된 경우 지정된 헤더 필드만 캐시할 수 없음 ex) `cache-control: no-cache=Location`

### no-store

`cache-control : no-store`

- Request 헤더에 쓰인 경우
    - 보내는 request 값을 캐시하지 말라는 뜻을 가짐
- Response 헤더에 쓰인 경우
    - 보내는 response 값을 캐시하지 말라는 뜻을 가짐

### public 과 private

`cache-control : public or private`

- CDN과 같은 중간 캐시 서버가 특정 리소스를 캐시할 수 있는지 여부를 지정하기 위해 사용
- public : 모든 사람(브라우저)과 중간 서버가 캐시를 저장할 수 있음
- private : 가장 끝의 사용자 브라우저만 캐시를 저장할 수 있음
- 기존의 max-age 값과 조합하려면 `Cache-Control: public, max-age=86400` 과 같이 콤마로 연결할 수 있음


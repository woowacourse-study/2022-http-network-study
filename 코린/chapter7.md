## 공개키 = 비대칭키

### 언제 쓰이나?

- HTTPS의 SSL에서 사용하는 암호화 방식

### 왜 나왔을까?

- 공통키(암호화, 복호화에 하나의 키를 사용하는 방식) 암호의 취약함을 보완하기 위하여
- 네트워크 환경에서 안전하게 공통키를 전달하는 방법은 없음
- 네트워크는 도청이 가능하기 때문
- 애초에 키를 안전하게 보낼 수 있다면 데이터를 암호화 할 필요가 없음

### 사용법

- 두 개의 키를 가짐 (Private Key, Public Key)

**Private Key**

- 공개돼서는 안되는 키
- Public Key로 암호화된 내용은 Private Key로 복호화 할 수 있음
- 즉, 암호화된 내용을 나만 알 수 있음

**Public Key**

- 공개되는 키
- Private Key로 암호화된 내용은 Public Key로 복호화 할 수 있음
- 즉, 누가 나에게 암호화된 내용을 보냈는지 검증할 수 있음

![KakaoTalk_Photo_2022-05-19-11-16-18.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a57b4f07-4405-4c0c-abf2-13df394d8d16/KakaoTalk_Photo_2022-05-19-11-16-18.png)

**종류**

- RSA
- ElGamal
- ECC
- DSA

**단점**

- 암복호화 속도가 오래 걸림 ↔ 공통키를 전달 할 때만 공개키로 암복호화를 하는 방식으로 처리

## HTTPS의 하이브리드 암호 시스템

모든 데이터 통신을 비대칭키로 하면 좋겠지만, 앞서 말했듯 비대칭키는 암복호화 처리 속도가 느림

HTTPS에서는 **대칭키를 전달할 때만 비대칭키로 암호화하여 전달**하고, 그 이후의 요청에서는 대칭키를 통해 통신함

1. 서버의 공개키 알아내기
    
![server의 공개키 알아내기.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a934c726-c579-421b-8a0b-e21e22984870/server의_공개키_알아내기.png)
    
    - 서버의 공개키를 인증기관에 등록하면 인증기관의 PrivateKey로 암호화된 공개키 증명서를 발급받을 수 있음
    - 발급받은 공개키 증명서를 클라이언트에게 전송
    - 클라이언트는 미리 브라우저에 저장되어있는 인증기관의 PublicKey로 공개키 증명서를 복호화
    - 복호화가 된다면 서버의 공개키를 알아낼 수 있음
2. 대칭키 만들기
    - 서버의 공개키를 알아내는 과정에서 서버와 클라이언트가 각각 랜덤 값을 발생시킴
    - 각 랜덤 값으로 클라이언트에서 Pre-Master secret key(대칭키)를 발행시킴
3. 서버의 공개키로 대칭키를 암호화하여 전송
    - 해당 Pre-Master secret key(대칭키)를 서버의 공개키로 암호화하여 서버에 전송함
    - 이로써 서버와 클라이언트는 안전한 방식으로 대칭키를 갖게 됨
4. 대칭키로 통신하기
    - 이후의 통신은 대칭키로 암복호화 하여 이루어짐

![1.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/47bf387c-7ac4-4abb-961b-43d25fe36639/1.png)

![2.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e4ba15cd-4b6a-4051-a4e6-4a95a3a6a613/2.png)

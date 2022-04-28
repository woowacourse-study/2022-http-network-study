## TCP와 UDP

### TCP의 특징
1. 용량이 큰 데이터를 보내기 쉽게 segment라고 불리는 단위 패킷으로 작게 분해하여 관리함
2. 신뢰성 있는 서비스를 보장
    - 3-way-handshaking : 패킷들이 전달 됐는지 여부를 상대에게 확인하는 것. SYN, ACK 이라는 TCP 플래그를 사용함.
    - 


![image](https://user-images.githubusercontent.com/61769743/165796487-97b90f5d-68fc-4450-97da-0f7a0a4c71fc.png)
- Syn 플래그로 상대에게 접속
- Syn/Ack 으로 송신측에 접속 및 패킷 수신 사실 알림
- Ack 플래그로 수신 사실을 확인하고 모든 패킷 교환이 완료됐음을 알림

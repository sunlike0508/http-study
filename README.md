# http-study

# 인터넷 네트워크

- 인터넷 통신
- IP (internet protocol)
- TCP, UDP
- Port
- DNS

## IP

IP 주소 부여 (패킷을 통한 메시지 전달)

출발 IP, 목적 IP, 메시지(전송데이터), 기타등등 -> 이 묶음을 패킷

### 한계

- 비연결성 : 패킷을 받을 대상이 없거나 서비스 불능 상태여도 패킷 전송
- 비신뢰성 : 중간에 패킷이 사라지면? 패킷이 순서대로 안오면?
- 프로그램으로 구분 : 같은 IP를 사용하는 서버에서 통신하는 애플리케이션이 둘 이상이라면?

## TCP, UDP

### 인터넷 프로토콜 스택의 4계층

애플리케이션 계층 (HTTP , FTP)
전송 계층 (TCP, UDP)
인터넷 계층 (IP)
네트워크 전송 계층 (LAN)

<img width="996" alt="Screenshot 2024-08-21 at 21 46 27" src="https://github.com/user-attachments/assets/4a02d4a2-fb69-4814-aa5b-c8d92c58d922">

### TCP

전송 제어 프로토콜(transmission control protocol)

* 연결지향 - TCP 3 way handshake (가상 연결)

<img width="808" alt="Screenshot 2024-08-21 at 21 49 33" src="https://github.com/user-attachments/assets/70dfbb6e-8226-4b7a-aec2-67ca3007c34e">

* TCP/IP 패킷 정보

<img width="871" alt="Screenshot 2024-08-21 at 21 52 19" src="https://github.com/user-attachments/assets/88e951e4-c1cc-482e-832d-7a6307a7e85b">

SYN: 접속 요청
ACK: 요청 수락
3. ACK 와 함께 데이터 전송

* 데이터 전달 보증

<img width="843" alt="Screenshot 2024-08-21 at 21 51 00" src="https://github.com/user-attachments/assets/39903960-55a3-4e22-9fb7-b3e8955911d6">

* 순서 보장

* 신뢰할 수 있는 프로토콜

* 현재 대부분 이것을 사용

### UDP

사용자 데이터그램 프로토콜(User Datagram Protocol)

* 하얀 도화지에 비유(기능이 거의 없음)
* 연결지향 X
* 데이터 전달 보증 X
* 순서 보장 X
* 데이터 전달 및 순서가 보장되지 않지만, 단순하고 빠름
* 정리
    * IP와 거의 같다. + PORT + 체크설 정도만 추가
    * 애플리케이션에서 추가 작업 필요
    * 요즘 각광 다시 받고 있다. 최적화가 많이 이루어짐.
 





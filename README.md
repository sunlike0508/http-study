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
   
   (3)ACK 와 함께 데이터 전송

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

## PORT

한번에 둘 이상 연결해야 한다면? (같은 클라이언트에 여러 애플리케이션을 사용한다면?)

0에서 65535 까지 할당 가능

FTP 20, 21

http 80

http 443

## DNS (Domain Name System)

IP는 변경될 수 있다.

도메인명과 IP가 매핑된 DNS서버가 있다.

# URI와 웹 브라우저 요청 흐름

## URI

Uniform Resource Identifier

리소스 식별하는 통일된 방식, 자원(URI로 식별할 수 있는 모든 것), 다른 항목과 구분하는데 필요한 정보

URL : locator (리소스가 있는 위치)
URN : Name : 리소스에 이름을 부여 (거의 잘 안쓴다. 보편화가 되지 않음)

### 전체 문법

• scheme://[userinfo@]host[:port][/path][?query][#fragment]

• https://www.google.com:443/search?q=hello&hl=ko

• 프로토콜(https)

• 호스트명(www.google.com)

• 포트 번호(443)

• 패스(/search)

• 쿼리 파라미터(q=hello&hl=ko)

* fragment : html 내부 북마크 등에 사용, 서버에 전송하는 정보 아님 (잘 사용 안함)







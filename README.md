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

• fragment : html 내부 북마크 등에 사용, 서버에 전송하는 정보 아님 (잘 사용 안함)

# HTTP

* Hyper Text Transfer Protocol

1.1 버전 : 1997년 출시, 이걸 거의 다 쓴다.

TCP : HTTP/1.1, HTTP/2

UDP : HTTP/3

## 특징

1) 클라, 서버 구조
2) stateless 비연결성 : 수평확장이 편리하다.
     * 로그인 개발에 힘듬 -> 쿠키, 세센등을 이용해서 상태 유지
     * 정적페이지 같은 걸로 이벤트(시간에 딱 맞추어 발생하는 몰리는 트래픽) 같은거 해결하려고 노력해야함.
  
3) 요즘은 영상도 http 이용한다.


### 구성

1) 시작라인
2) 헤더 : http 전송에 필요한 모든 부가 정보, 메시지 바디의 내용, 크기, 압축, 인증, 클라이언트 정보, 서버 정보, 캐시 관리 정보 등등
3) 메세지 바디


# HTTP Method

GET, POST, PUT, PATCH, DELETE

## 속성

### 안전

호출해도 리소스를 변경하지 않는다.

계속 호출해서 로그가 쌓여서 장애가 발생하면? 그런 부가적인것은 고려하지 않는다. 순수 리소스의 변경만 고려한다.

### 멱등성 (Idempotent)

f(f(x)) = f(x)

한 번 호출하든 두 번 호출하든 100번 하든 결과는 똑같다.

GET, PUT, DELETE : 멱등이다.

POST는 멱등이 아니다.

* 자동 복구 메커니즘 : 서버가 타임아웃등 정상 응답을 주지 못할때, 클라이언트가 같은 요청을 보낼 수 있다.

**멱등은 외부 요인으로 중간에 리소스가 변경되는것 까지는 고려하지 않는다.**

### 캐시가능

응답 결과 리소스를 캐시해서 사용해도 되는가?

GET, HEAD, POST, PATCH 캐시 가능. 그러나 현실적으로 GET, HEAD만 캐시가 가능. 그 외는 body로 인해 구현이 쉽지 않음


# HTTP Method 활용

multipart/form-data : 파일 업로드 같은 바이너리 데이터 전송시 사용

HTML Form 전송은 GET, POST만 지원

1) 정적 데이터 조회
2) 동적 데이터 조회
3) HTML FORM을 통한 데이터 전송
4) HTTP API 전송

* PUT : 클라이언트가 리소스 URI를 알고 있어야 한다. 즉, 클라이언트가 자원을 알고 관리한다는 의미.

* URI 설계 참고 사이트 : https://restfulapi.net/resource-naming

* HTTP 메서드로 표현하기 힘든 것들은 동사를 직접 사용 ex) html form에서 멤버 삭제 : /members/{id}/delete

# HTTP 상태코드

## 1xx (informational)

요청이 수신되어 처리중 (거의 사용 X)

## 2xx (Successful) 

요청 정상 처리

* 200 : OK
* 201 : Created, 새로운 리소스 생성 성공
* 202 : Accepted, 요청은 받았으나 아직 처리되지 않음. 배치 처리 같은 곳에서 사용. 잘 사용 X
* 204 : No content. 요청을 받아 수행했으나, 응답 payload에 보낼 데이터가 없음. ex) 웹 문서 편집기에서 save 버튼

## 3xx 

요청을 완료하려면 추가 행동이 필요

웹 브라우저는 3xx 응답의 결과에 Location 헤더가 있으면, Location 위치로 자동 이동(리다이렉트)

<img width="928" alt="Screenshot 2024-08-23 at 13 28 28" src="https://github.com/user-attachments/assets/5b6fff57-d357-4ad7-a9d2-9f64b83362ee">

• 300 Multiple Choices (잘 안씀)
• 301 Moved Permanently
• 302 Found
• 303 See Other
• 304 Not Modified
• 307 Temporary Redirect
• 308 Permanent Redirect


### 종류

1) 영구 리다이랙션 : 특정 리소스의 URI가 영구적으로 이동
   * 301 : 리다이렉트시 요청 메서드가 GET으로 변하고, 본문이 제거될 수 있음
   * 308 : 리다이렉트시 요청 메서드와 본문 유지(처음 POST를 보내면 리다이렉트도 POST 유지)
   * 회원 가입하려고 내용 기입하고 요청보냈는데 해당 요청 URI가 변경되어 새로운 페이지가 뜰때, 메시지가 유지되냐 안되냐 차이.
   * 두 개 모두 기능은 같음
   * 근데 둘다 거의 사용 안함.

2) 일시 리다이렉션 : ex) 주문 완료 후 주문 내역 화면으로 이동
   * 302 : 리다이렉트시 요청 메서드가 GET으로 변하고, 본문이 제거될 수 있음
   * 307 : 302이와 기능은 같음. 그러나 본문은 무조건 유지해야함
   * 303 : 302이와 같음. 요청 메서드가 GET으로 변경
   * 303, 307을 권장하지만 현실적으로 보통 디폴트로 302로 씀
   * PRG : Post / Redirect / Get
   * POST로 주문 후에 웹 브라우저를 새로고침하면?
   * 새로고침은 다시 요청
   * 중복 주문이 된다.
   

4) 특수 리다일렉션 : 결과 대신 캐시를 사용
   * 304 : 캐시를 목적으로 사용. 클라이언트에게 리소스가 수정되지 않았음을 알려준다. 따라서 클라이언트는 로컬pc에 저장된 캐시를 재사용된다
   * 304 응답은 메시지 바디를 포함하면 안된다. (당연히 로컬 캐시를 사용해야 하므로)

## 4xx

클라이언트 오류, 잘못된 문법등으로 서버가 요청을 수해할 수 없음

* 400 : Bad Request, 요청 구문, 메시지 등등 오류. API 스펙이 맞지 않을 때. 서버 개발자는 유효성 체크를 잘해야 함.
* 401 : Unauthorized. 클라이언트가 인증이 필요함. 인가가 아닌 인증이 안된것이다. 오해 ㄴㄴ
* 403 : Forbidden. 이게 인가. 인가가 안된 사람이 리소스 접근함.
* 404 : Not Found. 요청 리소스가 서버에 없음.


## 5xx

서버 오류, 서버가 정상 요청을 처리하지 못함

클라이언트가 재시도하면 성공할 수도 있음

* 500 : Internal Servever Error
* 503 : Service Unavailable, 서버가 일시적 과부하.

# HTTP 헤더

http 전송에 필요한 모든 부가정보를 가지고 있음

헤더의 표준이 너무나 많음.

## 헤더 분류

RFC2616 (1999년) 이게 표준이었는데 이제 폐기

FRC723X (2015년)으로 변화

엔티티라는 말을 표현이라고 변경(요청이나 응답에 전달할 실제 데이터)

표현 헤더는 표현 데이터를 해석할 수 있는 정보 제공

메시지 본문 (message body) -> payload 라고 변경

### 표현

표현 헤더는 전송, 응답 둘다 사용

### 협상 

클라이언트가 선호하는 표현 요청

협상 헤더는 요청시에만 사용

ex) Accept-Language : 클라이언트가 선호하는 자연언어

1) 우선순위1

Quality Values 값 사용

0 ~ 1 클수록 높은 우선순위

생략하면 1

ex) Accept-Language: ko-KR,ko;q=0.9,en-US;q=0.8,en;q=0.7

2) 우선순위2

구체적인 것이 우선한다.

Accept: text/*, text/plain, text/plain;format=flowed, */*

text/plain;format=flowed 이게 1순위, 그 다음 text/plain

3) 우선순위3

구체적인 것을 기준으로 미디어 타입을 맞춘다.

여기까진 잘 안쓴다.


### 전송 방식

단순 전송

압축 전송 : content-encoding : gzip

분할 전송 : 헤더에 transfer-encoding : chunked 이렇게 보냄, content-length 필요없음

범위 전송

### 일반 정보

* From : 유버 에이전트의 이메일 정보, 잘 사용 안함
* Referer : 이전 웹 페이지 주소. 유입 경로를 알 수 있음. 원래는 referreer의 오타. 근데 굳어져버려서 이렇게 쓰는 중
* User-Agent : 클라이언트 애플리케이션 정보
* Server : 요청을 처리하는 origin 서버의 소프트웨어 정보.
* Date : 메시지가 발생한 날짜와 시간

### 특별한 정보

* host : 요청한 호스트 정보(도메인). 필수. 하나의 서버에 여러 개의 가상호스트를 운영할때 유용.
* location : 페이지 리다이랙션. 201, 3xx 에서 많이 쓰임
* allow : 허용 가능한 http 메서드, 405에서 응답에 포함해야 함. 잘 안씀
* retry-after : 유저가 다음 요청을 하기까지 기다려야 하는 시간.

### 인증

* Authorization : 클라이언트 인증 정보를 서버에 전달,
   * Authorizatino : Basic xxxxxx
* WWW-Authenticate : 리소스 접근 시 필요한 인증 방법 정의, 401과 응답에 함께 사용.

### 쿠키

* Set-Cookie : 서버에서 클라이언트로 쿠키 전달(응답)
* Cookie : 클라이언트가 서버에서 받은 쿠키를 저장하고, http 요청시 헤더로 전달

* 주 사용처
   * 로그인
   * 광고 정보 트래킹
* 쿠키 정보는 항상 서버에 전송됨
   * 네트워크 트래픽 추가 유발
   * 최소한의 정보만 사용(세선id, 인증 토큰)
   * 서버에 전송하지 않고 웹 브라우저 내부에 데이터를 저장하고 싶으면 웹 스토리지 사용
 
***보안에 민감한 데이터는 저장하면 안된다. (주민번호, 신용카드 번호 등등)***

#### 생명주기

Expires : 만료일 되면 쿠키 삭제, GMT 기준으로 넣어줘야함.

max-age : 음수 넣으면 쿠키 삭제

#### 도메인

• 예) domain=example.org
• 명시: 명시한 문서 기준 도메인 + 서브 도메인 포함
   • domain=example.org를 지정해서 쿠키 생성
   • example.org는 물론이고
   • dev.example.org도 쿠키 접근
• 생략: 현재 문서 기준 도메인만 적용
   • example.org 에서 쿠키를 생성하고 domain 지정을 생략
   • example.org 에서만 쿠키 접근
   • dev.example.org는 쿠키 미접근

#### 경로

 ex) path=/home

이 경로를 포함한 하위 경로 페이지만 쿠키 접근

일반적으로 path=/루트로 기정

#### 보안

* Secure
   * http, https를 구분하지 않고 전송
   * 이걸 적용하면 https인 경우에만 전송
 
* httpOnly
   * XSS 공격 방지
   * 자바스크립트에서 접근 불가
   * http 전송에만 사용
 
* SameSite
   * XSRF 공격 방지
   * 요청 도메인과 쿠키에 설정된 도메인이 같은 경우만 쿠키 전송
 
## 캐시 

캐시 시간이 초과되면?

1) 서버가 다시 데이터를 전달한다.
2) 캐시 시간만 연장해준다.

### 검증 헤더 추가

* Last-Modified : 데이터가 마지막에 수정된 시간 (서버에서 보내는 값)
* if-modified-since : 클라이언트에서 last-modified가 있는지 확인하고 여기에 담아서 서버에 보냄
* 그럼 서버에서 데이터가 변경된게 없다면 304(Not-Modified)로 보냄
* 클라이언트에서 304 응답을 받고 가지고 있던 캐시데이터 사용

이렇게 하면 응답 데이터를 줄일 수 있다.

1초 미만 단위 캐시는 안된다. (근데 뭐 1초 미만은... 거의...)

데이터를 수정했는데 그 데이터가 기존이랑 같다면, 불필요한 응답을 다시 보내야함. (날짜로만 체크하기 때문에)

이 문제를 해결하기 위해서? ETag

### 검증 헤더 추가2

ETag (Entity Tag) : If-None Match

* 캐시용 데이터에 임의의 고유한 버전 이름울 달아둠
* 데이터가 변경되면 이 이름을 바꾸어서 변경함(Hash를 다시 생성)
* ETag가 다르면 다시 받고 아니면 캐시사용이라는 이야기

## 캐시 제어 헤어

### Cache-Control : 캐시 지시어

* max-age : 캐시 유효 시간, 초단위
* no-cache : 데이터는 캐시해도 되지만, 항상 origin 서버에 검증하고 사용해라
* no-store : 데이터에 민감한 정보가 있으므로 저장하면 안됨

### Pragma

잘 안씀

### Expires

캐시 만료일 지정, 대신 max-age 사용 권장

## 프록시 캐시

### Cache-Control : 캐시 지시어

* public : public 캐시에 저장되어도 됌
* private : 해당 사용자만 저장 가능

## 캐시 무효화

확실한 캐시 무효화 응답

* no-cache
* no-store
* must-revalidate : 캐시 만료 후 최초 조회시 origin 서버에 검증해야 함

no-cache랑 must-revalidate 차이 : 중간에 프록시 캐시에서 원서버로 갈때 오류가 발생하면, 응답을 정상으로 보여주면 no-cache, 실패를 보내면 must

물론 이것도 프록시 캐시에서 설정해야한다. no-cache가 성공으로 보내는 이유는 그냥 실패보단 캐시 사용해도 된다는 의미의 no-cache 이니까 성공으로 보내는게 낫다고 판단해서 그렇다.

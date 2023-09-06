# 목차
1. [Protocol](#1-protocol)
2. [OSI 7계층, TCP/IP 4계층](#2-osi-7계층-tcpip-4계층)
3. [Port, well known port](#3-port-well-known-port)
4. [HTTP, URL](#4-http-url)
5. [TCP/IP](#5-tcpip)
6. [UDP / TCP 차이](#6-udp--tcp-차이)
7. [SSH, Telnet](#7-ssh-telnet)
8. [DNS](#8-dns)
9. [공인 IP, 사설 IP](#9-공인-ip-사설-ip)
10. [포트포워딩, 내부포트, 외부포트](#10-포트포워딩-내부포트-외부포트)
11. [내 PC에 Nginx 설치 후 포트포워딩하여 내 휴대폰으로 접속해보기](#11-내-pc에-nginx-설치-후-포트포워딩하여-내-휴대폰으로-접속해보기)
12. [내 핸드폰에서 PC로 어떤 과정을 거쳐서 접속 되는지 그려보기](#12-내-핸드폰에서-pc로-어떤-과정을-거쳐서-접속-되는지-그려보기)

## 1. Protocol
* 서로 다른 시스템 및 기기 간 데이터 교환을 원활히 하기 위한 표준화된 통신규약\
  `사용자 별로 환경이 다르고 통신의 규칙이 없으면 충돌, 지연 등 여러가지 문제가 발생할 수 있기 때문`
  
* 흐름 제어, 오류 제어 등 다양한 기능을함

## 2. OSI 7계층, TCP/IP 4계층

* OSI가 이론적 표준이라면 TCP/IP는 실무적 표준
* TCP/IP는 인터넷 개발 이후 계속 표준화되어 신뢰성이 우수인 반면, OSI 7 Layer는 표준이 되기는 하지만 실제적으로 구현되는 예가 거의 없어 신뢰성이 저하

### OSI 7계층
*물리 계층(Physical Layer)*
  - 물리 계층에서는 주로 전기적, 기계적, 기능적인 특성을 이용하여 통신 케이블로 데이터를 전송
  - 데이터를 전달만 할 뿐 다른 기능은 하지 않음
  - 장비 : 리비터(신호증폭), 허브(멀티포트), 케이블

*데이터링크 계층(Data Link Layer)*
  - 수신되는 정보의 오류와 흐름을 관리하여 안전한 정보의 전달을 수행할 수 있도록 도와주는 역할
  - 오류제어, 흐름제어 등의 기능을함
  - 랜에서 데이터를 정상적으로 주고받기 위해 필요한 계층이다. 그 규칙들 중 가장 많이 사용되는 규칙은 이더넷(Ethernet)
  - Mac 주소(컴퓨터의 물리적 주소,하드웨어 주소)를 가지고 통신, 데이터 전송되는 단위는 프레임(Frame)
    - 실질적인 통신, ip주소는 최적의 경로를 찾는 라우팅하는 주소, ip주소가 없으면 Mac 주소를 찾기 위해 전세계 mac 주소를 다 뒤져야
  - 장비 : 스위치, 브릿지

*네트워크 계층(Network Layer)*
  - 데이터를 목적지까지 가장 안전하고 빠르게 전달하는 기능(라우팅),  네트워크상에서 주소를 이용하여, 통신 데이터를 목적지까지 보낼 최적의 경로를 선택하는 과정을 말한다
  - 수신 측 주소를 가지고 경로 설정을 하여 목적지까지 찾아가게 하는 기능
  - 데이터의 구조는 패킷
  - 장비 : 라우터, L3 스위치
  - 프로토콜 : ARP, IP, ICMP, IGMP

*전송 계층(Transport Layer)*
  - 종단간(end-to-end) 통신을 다루는 계층으로 종단간 신뢰성 있고 효율적인 데이터를 전송하며, 기능은 오류검출 및 복구와 흐름제어, 중복검사 등을 수행한다.
  - 데이터 구조 : Segment
  - 장비 : L4 스위치(주요 기능 로드 밸런싱)
  - 프로토콜 : TCP, UDP, ARP

*세션 계층(Session Layer)*
  - 양 끝단의 프로세스가 데이터 통신(송수신)을 관리하기 위한 방법을 제시하는 계층
  - 프로토콜 : SSH, TLS

*표현 계층(Presentation Layer)*
  - 데이터 표현이 상이한 응용 프로세스의 독립성을 제공하고, 암호화
  - 프로토콜 : JPEG, MPEG, SMB, AFP
  
*응용 계층(Application Layer)*
  - 사용자가 보는 소프트웨어의 UI, 네트워크 서비스, 사용자의 입출력 부분 등을 담당하는 계층
  - 프로토콜 : DHCP, DNS, FTP, HTTP

### TCP/IP 계층
*Application Layer*
- 프로그램(브라우저)가 직접 인터액트하는 레이어. 데이터를 처음으로 받는곳. HTTP, SMTP등의 프로토콜을 가짐

*Transport Layer*
- 두 Host PC 간에 종단 간 연결을 맺고 데이터를 전달할 수 있는 기능을 수행

*Internet Layer*
- IP를 사용하여 데이터의 원천지(origin)과 목적지(destination)에 관한 정보를 첨부

*Network Layer*
- 알맞은 하드웨어로 데이터가 전달되도록 MAC주소를 핸들링, 데이터 패킷을 전기신호로 변환하여 선로를 통하여 전달할 수 있게 준비.

## 3. Port, well known port
### Port
* 컴퓨터가 각종 신호 또는 정보 등을 주고 받을 수 있도록 해주는 통신 통로
* 논리적인 접속 장소를 의미\
  `port가 없다면 하나의 서버는 하나의 서비스만 제공 가능`

### well known port
* 특정한 쓰임새를 위해서 IANA에서 할당한 TCP 및 UDP 포트 번호의 일부
- 0번 ~ 1023번 : 잘 알려진 포트 ( **well-known port** ), port번호는 UNIX/LINUX에서 root 권한으로만 port를 열 수 있음\
 (21 : FTP, 22 : SSH, 23 : TELNET, 80 : HTTP, 443 : HTTPS 등등)
- 1024번 ~ 49151번 : 등록된 포트 ( registered port ), 주로 서버 소켓으로 사용하는 영역
- 49152번 ~ 65535번 : 동적 포트 ( dynamic port ), 동적포트 영역으로 포트가 바인딩이 되는 영역이기때문에 서버포트로 사용하면 안됨

## 4. HTTP, URL
### HTTP(HyperText Transfer Protocol)
* HTML과 같은 하이퍼미디어 문서를 주로 전송했지만, 최근에는 Plain text, JSON, XML 등 다양한 형태의 정보도 전송하는 애플리케이션 레이어 프로토콜
* 무상태 프로토콜(Stateless)이며, 이는 서버가 두 요청 간에 어떠한 상태나 데이터를 유지하지 않음을 의미
  - 상태를 저장하지 않기 때문에 리소스 아낄 수 있음, 만약 로그인 시 매 요청 시 로그인을 요구할 수 있음\
  `해결책으로 쿠키나 세션을 이용`
* 비 연결성(Connectionless)으로 기본이 연결을 유지하는 않는 모델
  - 리소스를 아낄 수 있는 장점, 그러나 매번 요청에 대해 새로운 결을 해야 하므로 오버헤드가 발생\
  `해결책으로 KeepAlive속성을 이용하여 통신이 끝나고 지정된 시간동안 연결 유지시킴`
* HTTP Message는 다음과 같은 구조를 가지고 있음
![img1 daumcdn](https://user-images.githubusercontent.com/41093183/192709964-fe6fa455-f7fe-4cd9-8e89-a8156298371e.png)
* Method 종류
  - GET
    + 리소스를 조회할 때 사용
  - HEAD
    + GET과 동일한 형태로 요청을 보내지만 응답에서 메시지 바디를 제외하고 받음
  - POST
    + 서버에 데이터 처리를 요청할 때 사용
  - PUT 
    + 리소스를 대체할 때 사용 (리소스가 없으면 생성, 있으면 대체)
  - PATCH
    + 리소스의 데이터를 부분 변경할 때 사용
  - DELETE
    + 리소스를 삭제할 때 사용

### HTTP 버전 별 차이점
* HTTP 1.0
  - Method: GET, HEAD, POST
  - Connection 특성: 응답 직후 종료
  - Keep-Alive 사용 시 Connection:Keep-Alive 요청헤더를 보내야 함
  - 단기커넥션 : connection 하나 당 1 Request & 1 response 처리 가능, 
* HTTP 1.1
  - Method: GET, HEAD, POST, PUT, DELETE, TRACE, OPTIONS
  - Persistent connection : 내제, 지정한 timeout 동안 연속적인 요청 사이에 커넥션을 닫지 않음
  - pipelining : 하나의 커넥션에서 응답을 기다리지 않고 순차적인 여러 요청을 연속적으로 보낼 수 있음\
    `응답처리를 결국 미루는 방식으로 Head Of Line Blocking이라 부르며 pipelining의 문제점`
  - Multiple Connections : 클라이언트는 많은 양의 objects를 검색하는 성능을 높이기 위해 TCP 다중 연결을 함
* HTTP 2.0
  - Multiplexed Streams : HTTP/1.1의 PIPELINING의 개선으로 한 커넥션으로 동시에 여러 개의 메시지를 주고받을 수 있음, 요청 순서에 상관없이 먼저 완료된 순서대로 클라이언트에게 전달
  - Stream Prioritization : 클라이언트가 요청한 요청 본문에 CSS File , Image B, Image C 가 있다고 했을 때, CSS File의 전송이 늦어지는 경우 HTTP/2는 리소스 간의 우선순위를 판단하여 우선순위가 높은 것을 먼저 처리하여 지연을 줄임
  - Header Compression : HTTP/2는 Static/Dynamic Header Table 기법을 사용하여 중복 Header를 검출하고 중복되지 않는 Header 정보는 Huffman Encoding기법으로 인코딩하여 처리한다.
  - Server Push : 서버는 클라이언트가 요청하지 않은 리소스를 사전에 푸쉬를 통해 전송,  클라이언트가 추후에 HTML 문서를 요청할 때 해당 문서 내의 리소스를 사전에 클라이언트에서 다운로드할 수 있도록 하여 클라이언트의 요청을 최소화
  
https://jwdeveloper.tistory.com/218

https://bbo-blog.tistory.com/87?category=1004651


### URL
* URL은 Uniform Resource Location의 약자이며, 인터넷에 있는 자원을 나타내는 유일한 주소
* URI는 Uniform Resource Identifier의 약자이며, URI는 인터넷의 자원을 식별할 수 있는 문자열을 의미, 그 중 URL, URN이라는 하위 개념을 만들어서 특별히 어떤 표준을 지켜서 자원을 식별하는 것

## 5. TCP/IP
### TCP/IP
* TCP/IP(Transmission Control Protocol/Internet Protocol) : 인터넷으로 디바이스를 연결하는 네트워크 프로토콜의 집합이며 개별적인 네트워크 프로토콜로 사용될 수도 있음
* TCP/IP는 인터넷의 기본 통신 언어

### TCP
* 서버와 클라이언트 간에 데이터를 신뢰성있게 전달하기 위해 만들어진 프로토콜

### IP
* Internet Protocol : 네트워크 상에서 장비들을 구분하기 위한 주소


## 6. UDP / TCP 차이
### UDP
* UDP는 User Datagram Protocol : 비연결형, 신뢰성이 없는 전송 프로토콜
* 비연결성, 비신뢰성, tcp보다 빠름

### TCP
* TCP(Transmission Control Protocol) : 서버와 클라이언트간에 데이터를 신뢰성 있게 전달하기 위해 만들어진 프로토콜
* 순차 전송을 보장, 흐름 제어, 혼잡 제어, 오류 감지 등의 기능
* 연결지향 : TCP 3 Way Handshake을 통한 연결 수립
* 연결종료 : TCP 4 Way HandShake을 통한 연결 종료


## 7. SSH, Telnet
### SSH(Secure Shell)
* 22번 포트
* 원격 시스템에서 명령을 실행하고 다른 시스템으로 파일을 복사할 수 있도록 해주는 응용 프로그램 또는 그 프로토콜
* 보안적으로 암호화뒤 정보를 교환하기 때문에 보다 보안적인 면에서 뛰어남

### Telnet
* 23번 포트
* 원격지에 있는 시스템을 제어하기 위한 프로토콜
* 평문으로 데이터를 전송하기때문에 보안상 취약

## 8. DNS
* DNS(Domain Name System) : 도메인 네임과 함께 해당하는 IP 주소값을 한 쌍으로 저장하고 있는 데이터베이스
  - 도메인은 웹 브라우저를 통해 특정 사이트에 진입을 할 때, IP 주소를 대신하여 사용하는 주소

* 도메인 네임에서 IP를 얻는 방법
  - 1. 도메인이 브라우저 캐시에 들어있는지 확인
  - 2. hosts 파일에 매핑되어 있는지 확인
  - 3. DNS 서버에 요청

* DNS서버 IP 찾는 순서 (DNS서버는 계층화 되어있음)
  - 1. 로컬 DNS 서버에 www.naver.com 이 있으면 바로 IP 반환
  - 2. 없을 시 루트 DNS 서버에 문의 후 .com인 것을 확인 후 .com 등록된 DNS서버의 IP를 전달
  - 3. 로컬 DNS 서버는 www.naver.com를 .com DNS서버에게 문의, naver.com이 없으므로 해당 url을 관리하는 DNS 서버를 알려줌
  - 4. 로컬 DNS 서버는 www.naver.com를 .naver.com DNS서버에게 문의, 해당 주소가 있으므로 IP를 반환
  - 로컬 DNS 서버가 열 DNS 서버를 차례대로(Local DNS 서버 -> Root DNS 서버 -> com DNS 서버 -> naver.com DNS 서버) 물어보며 답을 찾는 과정을 Recursive Query
  - .com : 이것은 Top-level Domain Name이라고 부른다.
.naver.com : 이것은 Second-level Domain Name이라고 부른다.

https://it-mesung.tistory.com/180

## 9. 공인 IP, 사설 IP 
### 공인 IP
* 인터넷 업체가 사용자에게 할당하며 공유기가 인터넷과 통신하도록 하는 역할을 하는 외부 IP 주소
### 내부 IP
* 사설 네트워크에서 다른 장치와 안전하게 연결하기 위해 사용되며, 동일한 네트워크의 각 장치에는 고유한 사설 IP 주소가 할당\
  `IP주소의 고갈로 인해 LAN영역에 사설 IP를 할당`

* 사설 IP여도 인터넷 접속이 가능한 이유
  - NAT(Network Address Translation) : 출발지 사설 IP 주소를 출발지 공인 IP 주소로 바꿔주는 기술\
    `NAT만 사용하면 라우터에서 어느 host로 통신해야되는 구분이 안됨`
  - PAT(Port Address Tanslation) : NAT 에 포트번호 주소를 연동해서 사용할 경우, PAT를 이용하면 이론적으로는 1개의 공인 IP 에 65,536개의 사설 IP주소를 연결 시킬 수 있음

## 10. 포트포워딩, 내부포트, 외부포트
### 내부포트
* 외부에서 특정 포트로 접속한 기기를 내부의 어떤 포트 번호로 연결해 주느냐에 대한 포트 번호
### 외부포트
* 외부 장치가 해당 포트로의 장치로 접속 할 때 사용, 포트 포워딩 된 장비에 접속할 때 사용하는 포트 번호
### 포트포워딩 
* 인터페이스의 특정 포트로 들어온 패킷을 내부 네트워크에 존재하는 특정 단말의 특정 포트에 매핑해주는 기술\
  `외부에서 접속 시 공유기까지는 들어올 수 있지만 공유기에 연결된 pc는 사설 ip로 구성되어있기 때문에 알 수가 없음, 따라서 특정포트로 들어왔을 때 해당하는 host로 보내줌`
  
## 11. 내 PC에 Nginx 설치 후 포트포워딩하여 내 휴대폰으로 접속해보기
* 서버의 IP를 알기위해서 ipconfig/all 검색\
![image](https://user-images.githubusercontent.com/41093183/192748600-2a364523-eb0e-44b3-a21b-501b51b5be01.png)

* 외부에서 접속할 IP를 알아보기
  - 공유기를 사용할 경우 브라우저에서 게이트웨이 주소로 접속하면 공유기 페이지를 이용할 수 있음
  - ![image](https://user-images.githubusercontent.com/41093183/192751304-ba05e5ba-c185-4ca6-819a-4467ea97861e.png)
  - 위의 WAN의 IP가 외부에서 접속할 수 있는 IP

* 포트포워딩(12355 -> 80)
![image](https://user-images.githubusercontent.com/41093183/192749984-eebe849b-bbcb-4f71-a4d5-60d5eb284174.png)

* nginx 설치 후 실행
  - 설치 후 로컬에서 테스트 시 http://localhost/ 접속 시 성공, 실제 IP로 접속 시 접속 불가
  - nginx.conf에서 localhost -> 내 컴퓨터 IP로 세팅 후 IP로 접속 확인\
![image](https://user-images.githubusercontent.com/41093183/192752176-18f57f41-72b5-4eb3-aebe-e6bb54a5e212.png)


* 핸드폰에서 접속 시\
![image](https://user-images.githubusercontent.com/41093183/192752010-8da02167-41a4-48ff-81ed-7bba7bbc4aef.png)



## 12. 내 핸드폰에서 PC로 어떤 과정을 거쳐서 접속 되는지 그려보기
![image](https://user-images.githubusercontent.com/41093183/193053221-05db6ff9-3549-464e-84da-0f4dc25e295c.png)

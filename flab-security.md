# 목차
1. [Port에서 Well Known Port 말고 다른 포트들은 무엇이 있는지 알아보세요.](#1-port에서-well-known-port-말고-다른-포트들은-무엇이-있는지-알아보세요)
2. [암호화, 복호화](#2-암호화-복호화)
3. [대칭키 암호](#3-대칭키-암호)
4. [비대칭키 암호](#4-비대칭키-암호)
5. [HTTPS가 어떻게 암호화된 통신을 할 수 있는지?](#5-https가-어떻게-암호화된-통신을-할-수-있는지)
6. [해시(Hash)를 왜 쓰는지](#6-해시hash를-왜-쓰는지)
7. [많이 사용되는 해시 알고리즘들](#7-많이-사용되는-해시-알고리즘들)

## 1. Port에서 Well Known Port 말고 다른 포트들은 무엇이 있는지 알아보세요.
### 잘 알려진 포트 ( well-known port )
- UNIX/LINUX에서 root 권한으로만 port를 열 수 있음
- 0번 ~ 1023번 (주요 포트 - 21 : FTP, 22 : SSH, 23 : TELNET, 80 : HTTP, 443 : HTTPS 등등)

### 등록된 포트 ( registered port )
- 주로 서버 소켓으로 사용하는 영역
- 1024번 ~ 49151번

### 동적 포트 ( dynamic port )
- 동적포트 영역으로 포트가 바인딩이 되는 영역이기때문에 서버포트로 사용하면 안됨
- 49152번 ~ 65535번

## 2. 암호화, 복호화
### 암호화란 ?
- 평문에 암호기술을 적용하여 암호문으로 변환하는 과정

### 복호화란 ?
- 다시 평문으로 복원하는 과정을 복호화

### 암호화 종류 
  - 단방향 암호화 : 암호화 후 복호화 불가, 해시방식
  - 양방향 암호화 : 암호화와 복호화 모두 가능한 것이 특징, 대칭키, 비대칭키 방식이 대표적

## 3. 대칭키 암호
### 대칭키 암호란 ?
- 암ㆍ복호화에 같은 암호 키를 사용하는 알고리즘 (AES, DES, SEED 등)

### 특징 
- 내부 구조가 간단한 치환과 전치의 조합으로 되어 있어 연산 속도가 빠르다는 장점
- 송ㆍ수신자 간에 동일한 키를 공유해야 하므로 많은 사람들과의 정보 교환 시 많은 키를 관리해야 하는 어려움
- 키 배송 문제(키를 전달 시 보안 문제가 발생함)
  
## 4. 비대칭키 암호
### 비대칭키 암호란 ?
- 암·복호화에 서로 다른 키를 사용하는 알고리즘(PKI, RSA)
- 공개키(Public Key)와 개인키(Private Key)가 하나의 쌍을 이루고 있다
  + 공개키 :  다른 사람들에게 공개된 키로서 정보를 암호화할 수 있는 키
  + 개인키 : 사용자 본인만 알고 있어서 암호를 풀 수 있는 키

### 특징
- 복잡한 연산을 사용하기 때문에 대칭키 암호보다 느림
- 키 분배 필요 없음
  - 전자 서명(Digital Signature) :  인터넷 상에서 본인임을 증명하기 위해 서명을 하는 수단 (ssl 인증서)
    + 공개키 암호를 거꾸로 활용하는 방식
    + 송·수신자의 역할이 반대로 되어, 개인키를 소유한 사람만이 전자 서명 알고리즘을 통해 평문에 대한 서명 값을 생성
    + 생성된 서명 값에 대하여 공개키를 이용하면 평문을 검증할 수 있기 때문에, 누구나 그 서명을 검증할 수 있게 됨

### 활용
- 전자 서명(Digital Signature) : 인터넷 상에서 본인임을 증명하기 위해 서명을 하는 수단 (ssl 인증서)
  + 공개키 암호를 거꾸로 활용하는 방식
  + 송·수신자의 역할이 반대로 되어, 개인키를 소유한 사람만이 전자 서명 알고리즘을 통해 평문에 대한 서명 값을 생성
  + 생성된 서명 값에 대하여 공개키를 이용하면 평문을 검증할 수 있기 때문에, 누구나 그 서명을 검증할 수 있게 됨

## 5. HTTPS가 어떻게 암호화된 통신을 할 수 있는지?
### HTTPS란 ?
- HTTPS는 HTTP over Secure Socket Layer 의 약자로 즉 SSL(Secure Socket Layer)을 이용한 HTTP 통신 방식을 의미
- HTTP의 보안 문제점(평문 통신, 변조 가능성 등)을 SSL(Secure Socket Layer, 보안 소켓 계층)을 사용하여 해결함

### SSL란 ?
- SSL은 통신 패킷을 암호화하여 패킷 탈취, 정보 누출 등을 방지하기 위한 보안 프로토콜
- SSL 3.0까지 발표, 3.0을 표준화한 것이 TLS라고 함
- 보안, 성능의 이유로 공개키 암호화 방식과 공개키의 단점을 보완한 대칭키 암호화 방식을 함께 사용

------------------
### HTTPS HandShake 요약
![img1 daumcdn](https://user-images.githubusercontent.com/41093183/193241810-51c9debb-9141-465f-9020-02807a7a2056.png)


- 클라이언트측에서 ClientHello 암호화 알고리즘 나열 및 전달\
  (브라우저가 사용 및 지원하는 SSL,TLS 버전정보,암호화방식(cipher suite),난수 등 전달)
- 서버측에서 ServerHello 암호화알고리즘 선택, SSL 인증서 클라이언트에게 전달\
  (cipher suite 선택, 서버 공개키 담긴 SSL 인증서 전달, 난수 전달 등)
- 클라이언트측에서 Client Key Exchange 임시 대칭키 서버에게 전달\
  (CA 공개키로 서버 인증서를 복호화, 클라이언트와 서버의 난수를 이용해서 Premaster Secret생성 -> 서버 공개키로 임시 대칭키 생성)
- 서버측에서 받은 임시 대칭키 복호화 후 Master Secret 생성하고 session key를 생성, 이 키를 이용하여 데이터 암호화
------------------

### HTTPS HandShake 과정

**1. Client Hello (클라이언트 -> 서버)**

  - 브라우저(클라이언트) 마다 지원하는 암호화 알고리즘과 TLS 버전이 다르므로 해당 정보를 전송하며, 난수 값을 생성하여 전송
  - random : 클라이언트는 32바이트 난수값을 전달. 이 랜덤값은 나중에 비밀 데이터를 위해 사용이 됨. 비밀 데이터를 master secret이라고 함
  - session ID : 세션을 처음 생성할때는 빈값, 이미 생성된 세션이 있다면 그 세션 ID를 전달함
  - cipher suite : 클라이언트가 지원가능한 키 교환 알고리즘, 대칭키 암호 알고리즘, 해시 알고리즘 등을 알려줌
     + EX) TLS_RSA_WITH_AES_128_GCM_SHA256 : 보통 이런식인데, 키 교환 알고리즘은 RSA, 대칭키 알고리즘은 AES_128 GCM방식을 사용하고 Hash 알고리즘으로는 SHA256을 사용한다는 것

\
**2. Server Hello (서버 -> 클라이언트)**

  - 사용할 TLS버전, 클라이트, 서버 공통으로 지원가능한 최적의 Cihper suite, 압축 방식 등을 client에게 전달
  - random : 역시 server도 32바이트 난수를 생성해서 client에게 전달, master secret이라는 비밀값을 생성할때 사용되는 재료
  - session ID : 세션 정보를 보냄

\
**3. Certificate (서버 -> 클라이언트)**

  - CA로 부터 발급받은 인증서(CA서버의 개인키로 암호화 되어있음)를 전송
  - 이 인증서를 이용해서 클라이언트는 서버가 믿을 만한, 신뢰할 만한 서버인지 확인
  - 클라이언트에 내장된 CA의 공개키로 복호화함 : 복호화가 되면 CA의 개인키로 암호화된 문서임을 암시적으로 보증

\
**4. Server Key Exchange (서버 -> 클라이언트)**

  - 키 교환에 필요한 정보를 제공, 만약 필요하지 않으면 이 과정은 생략이 가능
  - (서버의 공개 키가 SSL 인증서 내부에 없는 경우, 서버가 직접 전달한다는 뜻, 공개 키가 SSL 인증서 내부에 있을 경우 Server Key Exchange는 생략)

\
**5. Certificate Request (서버 -> 클라이언트)**

  - 서버가 클라이언트를 인증해야할때 인증서를 요구하는 단계,요청하지 않을수도 있음
  - (일반적으로 웹서버에 SSL을 설정할 때는 하지 않음)

\
**6. Server Hello Done (서버 -> 클라이언트)**

  - 서버의 말 종료

\
**7. Client Certifiacte (클라이언트 -> 서버)**

  - 서버에서 Certificate Request을 요청했으면, 인증서를 줌, 아니면 해당 없음

\
**8. Client Key Exchange (클라이언트 -> 서버)**

  - CA는 개인키로 암호화되어있음
  - 서버에게 받은 인증서를 CA의 공개키를 이용하여 복호화하고, 복호화된 인증서에는 서버의 공개키가 존재함, 서버의 공개키로 자신이 만든 난수와 서버가 만든난수를 통해 pre-master-secret를 생성함
  - 이 임시대칭키를 서버의 공개키로 암호화해서 서버로 전송

\
**9. Certificate verify (클라이언트 -> 서버)**

  - 클라이언트에 대한 Certificate request를 받았다면 보낸 인증서에 대한 개인키를 가지고 있다는 것을 증명, handshake과정에서 주고 받은 메시지 + master secret을 조합한 hash값에 개인키로 디지털 서명하여 전송

\
**10. Change Cipher Spec (클라이언트 -> 서버)**
  - 협상된 보안 파라미터를 적용하거나 변경될때 서버에게 알림

\
**11. Finished (클라이언트 -> 서버)**
  - 클라이언트 끝

\
**12.  Change Cipher Spec (클라이언트 -> 서버)**
  - 클라이언트로 부터 전송받은 pre-master-secret를 정상적으로 복호화 후 master-key(대칭키)로 승격 후 보안 파라미터를 적용하거나 변경될때 보내는 알림

\
**13. Finshed (클라이언트 -> 서버)**
  - 클라이언트 끝

<https://reakwon.tistory.com/106>\
<https://mysterico.tistory.com/30>\
<https://run-it.tistory.com/29>\
<https://dkrnfls.tistory.com/361>\
<https://steady-coding.tistory.com/512>



## 6. 해시(Hash)를 왜 쓰는지
### 해시 함수란?
- 해시 함수(Hash Function)는 임의의 길이의 메시지를 입력으로 받아 고정된 길이의 해시 값을 출력하는 함수

### 특징
- 입력값이 일부만 변경되어도 전혀 다른 해시값을 출력한다. [눈사태 효과], 목적은 메시지의 오류나 변조를 탐지할 수 있는 무결성
- 입력값 상관없이 고정된 길이의 해시값을 출력
- 복호화 불가능 [단방향 암호화 기법의 특징]
- 복잡하지 않은 알고리즘으로 구현되기 때문에 상대적으로 CPU, 메모리 같은 시스템 자원을 덜 소모함
- 같은 입력값에 대해서는 같은 출력값을 보장

### 활용
- 비밀번호, 전자서명, 전자투표, 전자상거래와 같은 민감한 입력의 무결성을 검증할 때 사용
- 해시테이블(hash table)이라는 자료구조에 사용




## 7. 많이 사용되는 해시 알고리즘들
### 대표적인 해시 함수
- MD5, HAS-160, SHA-1, SHA-2, SHA-3 등이 있음


  - MD5 (Message-Digest algorithm 5)
    + 임의의 길이를 입력받아 128bit 길이의 해시값을 출력
    + 단방향 알고리즘
    + 현재는 심각한 보안 문제로 인하여 MD5를 보안 관련 용도로 사용하지 않음


  - SSH (Secure Hash Algorithm, 안전한 해시 알고리즘)
    + 처음 SHA-0으로 정의되어 발표되었지만 바로 위험성이 발견되어 이를 개선한 SHA-1이 발표되었고, 널리 사용됨
    + SHA-1 역시 충돌을 이용한 위험성이 발견되어 SHA-2가 발표됨
    + SHA-2는 해시 길이에 따라 SHA-224, SHA-256, SHA-384, SHA-512 비트를 선택해서 사용, 해시 길이가 길수록 더 안전함

## 1. Telnet으로 아무 웹 페이지나 HTTP 요청을 보내보세요.
- **naver.com 80포트로 요청**\
![image](https://user-images.githubusercontent.com/41093183/194268460-a13da6cc-fc17-4115-b8c0-c34a6dc1b94b.png)

- **접속 후 아래 명령어 입력**\
![image](https://user-images.githubusercontent.com/41093183/194268767-86c35ca0-2481-4516-af80-69521dc46533.png)

- **302 응답으로 리다이렉트 응답을 받음**\
![image](https://user-images.githubusercontent.com/41093183/194269428-55431534-5858-4e60-b6c8-0443c573e93c.png)

- location 값이 https://www.naver.com/err/notfound.html 된 것으로 보아 http를 https로 리다이렉트 응답을 내보내줌
- 텔넷은 헤더를 분석하여 대응 할 수 없고 302코드도 해석이 안되기 때문에 연결이 종료됨

------------------

- **로컬테스트**
  - 8091 port로 LISTEN
  - telnet 192.168.56.1 8091 접속 후 GET /test.html HTTP/1.1 테스트 시\
![image](https://user-images.githubusercontent.com/41093183/194272885-1dec6d59-1ec9-4403-8e9c-90e82bac2cb7.png)

- **http->https 환경 맞추고 테스트**
  - http 8091 port로 LISTEN
  - https 8092 port로 LISTEN
  - http -> https 리다이렉트 설정(브라우저 테스트 시 http -> https로 리다이렉트 되는 것 확인)\
![image](https://user-images.githubusercontent.com/41093183/194274679-24fc91cb-0b8d-42a8-bffc-1824b098b0cd.png)

  - telnet 192.168.56.1 8091 접속 후 GET /test.html HTTP/1.1 테스트 시\
![image](https://user-images.githubusercontent.com/41093183/194273945-eb60aab5-855f-4f2c-aaff-1870294fda41.png)

  - naver.com 테스트 때와 똑같이 302 코드와 함께 location값이 https로 변경되어 리다이렉션하여 접속하라는 메시지가 옴

## 2. 시저암호 코딩
https://github.com/gggorock/flab-mentoring-records/blob/main/src/study/seungjae/caesar_cipher/Caesar.java


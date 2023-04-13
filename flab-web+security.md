## 목차
1. [웹 크롤러는 무엇을 하는건지?](#1-웹-크롤러는-무엇을-하는건지)
2. [크롤링된 데이터로는 무엇을 할 수 있는지?](#2-크롤링된-데이터로는-무엇을-할-수-있는지)
3. [User-Agent 헤더](#3-user-agent-헤더)
4. [robots.txt](#4-robotstxt)
5. [HTTP/1.1+, HTTP/2.0, HTTP/3.0에 대해](#5-http11-http20-http30에-대해)
6. [RFC 문서란 무엇인가?](#6-rfc-문서란-무엇인가)
7. [클라이언트에게 특정 쿠키를 사용하도록 지정하려면 서버에서 어떻게 하면 되는가?](#7-클라이언트에게-특정-쿠키를-사용하도록-지정하려면-서버에서-어떻게-하면-되는가)
8. [HTTP 기본 인증이란 무엇인가?](#8-http-기본-인증이란-무엇인가)
9. [인증과 인가는 무슨 차이인가?](#9-인증과-인가는-무슨-차이인가)
10. [다이제스트가 무엇인가?](#10-다이제스트가-무엇인가)
11. [특정 패킷의 재전송을 방지하기 위해 Nonce가 어떻게 사용되는가?](#11-특정-패킷의-재전송을-방지하기-위해-nonce가-어떻게-사용되는가)
12. [사전(Dictionary) 공격이란 무엇인가?](#12-사전dictionary-공격이란-무엇인가)
13. [무차별 대입(Brute Force) 공격이란 무엇인가?](#13-무차별-대입brute-force-공격이란-무엇인가)
14. [SQL 인젝션이란 무엇인가?](#14-sql-인젝션이란-무엇인가)
15. [PreparedStatement가 어떻게 SQL 인젝션을 막을 수 있는지?](#15-preparedstatement가-어떻게-sql-인젝션을-막을-수-있는지)
16. [XSS, CSRF이란 무엇인가?](#16-xss-csrf이란-무엇인가)
17. [CORS란 무엇인가?](#17-cors란-무엇인가)
18. [JSESSIONID가 발급되는 과정을 개발자 도구를 통해 확인해보기](#18-jsessionid가-발급되는-과정을-개발자-도구를-통해-확인해보기)

## 1. 웹 크롤러는 무엇을 하는건지?
### 웹 크롤러란?
* 인터넷 상에 있는 자료들을 가져와 분석하기 쉬운 형태로 가공하는 컴퓨터 프로그램

### 사용 이유?
* 원하는 정보를 자동적으로 수집하기 위해서
* 업무 자동화

### 단점
* 네트워크에 트래픽을 증가시키고 서버에 과부하를 줄 수 있음
* 개인정보까지 수집해 갈 수 있음

## 2. 크롤링된 데이터로는 무엇을 할 수 있는지?
* 수 많은 웹 사이트를 크롤링하여 검색서비스를 제공 ex) 구글
* 각종 소셜커머스 사이트를 크롤링 하여 최저가 정보 제공 ex) 쿠차
* 빅데이터 자료로 활용

## 3. User-Agent 헤더
### User-Agent 헤더란?
* HTTP 요청을 보내는 디바이스와 브라우저 등 사용자 소프트웨어의 식별 정보를 담고 있는 request header의 한 종류

### User-Agent 예시
``` Mozilla/5.0 (platform; rv:geckoversion) Gecko/geckotrail Firefox/firefoxversion ```
* Mozilla/5.0 : 접속한 브라우저가 Mozilla와 호환된다는 의미
* platform : 브라우저가 실행되는 운영체제 환경(window, mac, linux, android 등), 그리고 모바일인지 여부
* rv: geckoversion : Gecko 버전 (파이어폭스의 렌더링 엔진이다)
* Gecko/geckotrail : 브라우저가 Gecko 기반인지 여부. 데스크탑일 경우 geckotrail은 20100101이라는 스트링값으로 고정
* Firefox/firefoxversion : 브라우저가 파이어폭스라는 의미, 그리고 파이어폭스의 버전.

### 주 용도
* 웹 브라우저의 종류에 따라 다른 웹 페이지를 제공
* 운영체제의 종류에 따라 다른 콘텐츠를 표시
* 사용자가 사용중인 브라우저 및 운영 체제를 보여주는 통계를 수집
* 크롤링시 User-Agent 헤더를 조작하여 서버를 속일 수 있음

## 4. robots.txt
### robots.txt란
* 크롤러가 페이지에 요청을 해도 되거나, 요청을 해서는 안되는 경로를 적어둔 File로 계속적인 접근으로 인한 과부하 혹은 적당하지 않은 정보를 가져가는 것을 막기 위한 규약들이 적혀 있음

### 불법 Crawler란?
* robots.txt에 정의된 규약들을 지키지 않고 데이터를 추출하거나, 추출한 데이터를 통해 이익을 취하는 크롤러


출처: https://kkyunstory.tistory.com/2 [껸스토리:티스토리]


## 5. HTTP/1.1+, HTTP/2.0, HTTP/3.0에 대해
### HTTP 1.0
  - Method: GET, HEAD, POST
  - Connection 특성: 응답 직후 종료
  - Keep-Alive 사용 시 Connection:Keep-Alive 요청헤더를 보내야 함
  - 단기커넥션 : connection 하나 당 1 Request & 1 response 처리 가능(순차적인 트랜잭션 처리에 의한 지연 발생)
### HTTP 1.1
  - Method: GET, HEAD, POST, PUT, DELETE, TRACE, OPTIONS
  - Persistent connection(지속 커넥션) : 내제, 지정한 timeout 동안 연속적인 요청 사이에 커넥션을 닫지 않음
  - pipelining : 하나의 커넥션에서 응답을 기다리지 않고 순차적인 여러 요청을 연속적으로 보낼 수 있음\
    * pipelining의 문제점 : 응답처리를 결국 미루는 방식으로 Head Of Line Blocking이라 부름
  - Multiple Connections : 클라이언트는 많은 양의 objects를 검색하는 성능을 높이기 위해 TCP 다중 연결을 함
### HTTP 2.0
  - Multiplexed Streams : HTTP/1.1의 PIPELINING의 개선으로 한 커넥션으로 동시에 여러 개의 메시지를 주고받을 수 있음, 요청 순서에 상관없이 먼저 완료된 순서대로 클라이언트에게 전달
  - Stream Prioritization : 클라이언트가 요청한 요청 본문에 CSS File , Image B, Image C 가 있다고 했을 때, CSS File의 전송이 늦어지는 경우 HTTP/2는 리소스 간의 우선순위를 판단하여 우선순위가 높은 것을 먼저 처리하여 지연을 줄임
  - Header Compression : 이전 Header의 내용과 중복되는 필드를 재전송 하지 않도록 하여, 데이터를 절약함. 또한 기존에 HTTP Header가 Plain Text(평문)이었지만, HTTP/2에서는 Huffman Encoding 이용하여 데이터 전송 효율을 높임
    * Huffman Encoding : 문자 빈도수를 이용해서 파일을 압축하는 인코딩, 문자 빈도수가 많을수록 짧아지기 때문에 고정된 길이 보다 데이터의 크기가 작음
  - Server Push : 서버는 클라이언트가 요청하지 않은 리소스를 사전에 푸쉬를 통해 전송,  클라이언트가 추후에 HTML 문서를 요청할 때 해당 문서 내의 리소스를 사전에 클라이언트에서 다운로드할 수 있도록 하여 클라이언트의 요청을 최소화

### HTTP 1.1 VS HTTP 2.0
![multiplexing](https://user-images.githubusercontent.com/41093183/198871437-fa4ace2e-55f6-493a-81c1-2d895fd3151f.svg)


### HTTP 3.0
 - QUIC(Quick UDP Internet Connection)이라는 UDP 기반 프로토콜 위에서 돌아가는 HTTP
 - UDP는 하얀 도화지 같은 프로토콜로 커스텀 마이징에 용이함


  1) UDP 기반으로 TCP handshake 과정을 없앰
     * 데이터 전체를 첫 번째 라운드 트립에 포함해서 전송
     * 단, 클라이언트가 서버로 첫 요청을 보낼 때는 서버의 세션 키를 모르는 상태이기 때문에 목적지인 서버의 Connection ID를 사용하여 생성한 특별한 키인 초기화 키(Initial Key)를 사용하여 통신을 암호화
     * 한번 연결에 성공했다면 서버는 그 설정을 캐싱
  
  2) 패킷 손실 감지에 걸리는 시간 단축
     * TCP는 여러 ARQ 방식 중에서 Stop and Wait ARQ 방식으로 일정 시간이 경과해도 수신 측이 적절한 답변을 주지 않는다면 패킷이 손실된 것으로 판단하고 해당 패킷을 다시 보내는 방식
     * TCP에서 패킷 손실 감지에 대한 대표적인 문제는 타임 아웃을 언제 낼 것인가를 동적으로 계산해야한다는 것이고 이 때 필요한 것이 RTT(Round Trip Time) 정보임
     * 패킷 손실이 나면 RTT 계산이 애매해지고 TCP는 타임스탬프를 사용할 수 있는 상황이라면 타임스탬프를 통해 패킷의 전송 순서를 파악할 수 있지만, 만약 사용할 수 없는 경우 시퀀스 번호에 기반하여 암묵적으로 전송 순서를 추론할 수 밖에 없음
     * QUIC은 이런 불필요한 과정을 고유한 패킷 번호를 통해 패킷 손실 감지에 걸리는 시간을 단축함
  
  3) 멀티플렉싱을 지원
  4) 클라이언트의 IP가 바뀌어도 연결이 유지됨
     * QUIC은 Connection ID를 사용하여 서버와 연결을 생성하는데 Connection ID는 랜덤한 값일 뿐, 클라이언트의 IP와는 전혀 무관한 데이터이기 때문에 클라이언트의 IP가 변경되더라도 기존의 연결을 계속 유지할 수 있음

<br />
출처:https://evan-moon.github.io/2019/10/08/what-is-http3/

<br />

## 6. RFC 문서란 무엇인가?
### RFC 문서란?
* 미국의 국제 인터넷 표준화기구인 IETF에서 제공, 관리하는 문서로, 인터넷 개발에 있어서 필요한 기술, 연구 결과, 절차 등을 기술해놓은 메모
* 거의 모든 인터넷 표준은 항상 RFC로 문서화 되어 있음
* 누구나 RFC를 작성할 수 있으며 만약 문서가 IETF의 눈에 띄게 되고 문서의 신뢰가 높아지게 되면 IETF는 이 문서에 번호를 붙이게 되고 정식 RFC문서로 출판하게 됨

### 사용 이유?
* 표준을 정하기 위해

## 7. 클라이언트에게 특정 쿠키를 사용하도록 지정하려면 서버에서 어떻게 하면 되는가?
* 서버가 Set-Cookie 헤더를 통해 클라이언트가 사용할 쿠키를 전송할 수 있음
* 쿠키는 보통 브라우저에 의해 저장되며, 브라우저는 다음 요청 시 쿠키 헤더에 해당 쿠키를 추가하여 요청을 함
## 8. HTTP 기본 인증이란 무엇인가?
### HTTP 기본 인증이란?
* 서버가 클라이언트에서 인증 확인 정보(사용자 ID 및 비밀번호)를 요청할 수 있는 단순 인증 확인 및 응답 메커니즘
* 사용자가 누구인지 증명하는 작업
* HTTP의 자체 인증 기능을 이용

### 사용 이유?
* 사용자가 개인적인 데이터에 접근할 때 해당 사용자가 인증된 사용자인지 판별하기 위해 필요함

### 기본인증 과정
<img width="788" alt="69476371-7b604000-0e1c-11ea-8020-14bd69d8db2c" src="https://user-images.githubusercontent.com/41093183/198211826-d41fb5ca-c6f6-422f-bfde-7b26e75bb3c9.png">

**(a) 요청**: about.jpg 정보 요청 \
**(b) 인증요구**: 서버는 401 Unauthorized 응답과 함께 WWW-Authenticate 헤더를 기술해 어디서 어떻게 인증할지 설명 \
**(c) 인증**: 인코딩된 비밀번호와 그 외 인증 파라미터들을 Authorization 헤더에 담아 요청 보냄, 사용자 이름과 비밀번호를 입력해 세미클론으로 이어 붙여 Base64 인코딩 방식으로 인코딩해 같이 보내줌 
  - Base64로 인코딩하는 이유는 전송 중 원본 문자열이 변질될 걱정이 없고, (큰따옴표, 콜론, 캐리지 리턴)과 같은 HTTP헤더에서 사용할수 없는 정보를 보낼때도 유용하기 때문


**(d) 성공**: 인증이 완료되면, 상태코드와 함께 응답 반환 (추가적인 인증 알고리즘에 대한 정보를 Authenticate 헤더에 기술할수도 있음) 

#### 보안영역
* 웹 서버는 기밀문서를 보안 영역(realm) 그룹으로 나눔
* WWW-Authenticate헤더에 realm 지시자의 값
* realm을 보고 사용자가 권한의 범위를 이해하는데 도움이 되어야함

#### 프락시 인증
* 중개 프락시 서버를 통해 인증할 수도 있음
* 회사 리소스 전체에 대해 통합적인 접근 제어를 하기 위해 사용하면 좋음
* 웹 서버의 인증과 헤더와 상태 코드만 다르고 절차는 같음 \
![image](https://user-images.githubusercontent.com/41093183/198217065-fc0239c6-2361-4608-898c-494e420958b6.png)

### 기본 인증의 보안 결함
* base-64로 인코딩된 비밀번호는 쉽게 디코딩 될 수 있음 
  - 위의 문제를 해결하기 위해 모든 HTTP 트랜잭션을 SSL 암호화 채널을 통해 보내거나, 보안이 더 강화된 다이제스트 인증 같은 프로토콜 사용
* 제삼자가 인코딩된 사용자 이름과 비밀번호를 캡처해 그것을 그대로 원서버에 보내서 인증에 성공하고 서버에 접근할 수 있음
  - 기본 인증은 이러한 재전송 공격을 예방하기 위한 어떤 일도 하지 않음
* 프락시나 중개자가 중간에 개입하여 인증 헤더를 제외한 다른 부분을 수정해서 트랜잭션의 본래 의도를 바꾸면 정상적인 동작을 보장하지 않음
* 가짜 서버의 위장에 취약함

### 정리
* 기본 인증은 일반적인 환경에서 개인화나 접근을 제어하는데 편리함
* 어떤 리소스를 다른 사람들이 보지 않기를 원하기는 하지만, 보더라도 치명적이지 않은 경우 유용



<br />
<br />
출처:https://ideveloper2.dev/blog/2019-11-23--%EA%B8%B0%EB%B3%B8-%EC%9D%B8%EC%A6%9D-%EB%8B%A4%EC%9D%B4%EC%A0%9C%EC%8A%A4%ED%8A%B8-%EC%9D%B8%EC%A6%9D


## 9. 인증과 인가는 무슨 차이인가?
### 인증이란?
* 사용자가 누구인지 확인하는 절차
* ex) 회원가입, 로그인 과정


### 인가란?
* 사용자가 원하는 요청(Request)을 실행할 수 있는 권한 여부를 확인하는 절차
* 인증된 사용자에 대한 자원 접근 권한 확인
* ex) 게시판에 글을 쓸 때 해당 회원이 권한이 있는지 확인 과정

## 10. 다이제스트가 무엇인가?
### 다이제스트 인증이란?
* HTTP 기본 인증이 Base64 형태로 비밀번호를 실어서 보내는 단점을 보강하여 나온 인증 프로토콜
* 기본 인증과 호환되는 더 안전한 대체재

### 특징
* 비밀번호를 절대로 네트워크를 통해 평문으로 전송하지 않음
* 비밀번호를 안전하게 지키기 위한 "요약"을 사용
* 재전송 방지를 위한 난스(nonce) 사용

#### 단방향 요약
* 요약은 정보 본문의 압축이고, 단방향 함수로 동작
* 단방향 알고리즘은 암호화는 수행하지만 절대로 복호화가 불가능한 알고리즘을 말함
* 대표적인 요약 함수는 MD5이고, 임의의 바이트 배열을 원래 길이와 상관없이 128비트 요약으로 변환
* 요약 함수는 보통 암호 체크섬으로 불리며 단방향 해시함수이거나 지문함수

### 다이제스트 인증 핸드셰이크
<img width="873" alt="69477481-2a574880-0e2a-11ea-96be-ebda9de3e306" src="https://user-images.githubusercontent.com/41093183/198817172-9d909bca-4c7a-49e1-a752-6ae799d3dd36.png">

### 단점
* Hash 알고리즘으로 MD5를 사용하는데, 이 MD5는 보안 레벨이 낮기 때문에 미정부 보안 인증 규격인 FIPS인증 에서 인증하고 있지 않음, SHA-1,SHA1-244,SHA1-256 이상의 Hash 알고리즘을 사용하도록 권장
* MD5 Hash의 경우에는 특히나 Dictionary Attack에 취약

## 11. 특정 패킷의 재전송을 방지하기 위해 Nonce가 어떻게 사용되는가?
### Nonce란?
* 재전송 공격을 방지하기 위해 서버가 클라이언트에게 건네주는 자주 바뀌는(대략 1ms마다, 혹은 인증할 때마다) 증표

### 사용이유?
* 요약을 가로채서 서버로 몇번이고 재전송할 수 있기 때문에 요청 때 난스를 섞어줌

### 사용방법
* 비밀번호 요약을 만들 때 서버 측에서 보내준 난스를 섞어서 만들고, 서버측에서도 똑같은 난스를 섞어서 만든 요약을 비교
* 저장된 비밀번호 요약은 특정 난스값에 대해서만 유효함

## 12. 사전(Dictionary) 공격이란 무엇인가?
### 사전 공격이란?
* 공격자가 일반적으로 비밀번호에 많이 사용되는 단어나 문구를 사전(dictionary)처럼 만들어두고 무차별 대입으로 보안을 뚫는 기술
* 상당한 시간이 소요되는 무작위 순차 대입 방식의 단점을 극복 및 보완하는 방법으로, 미리 정의된 문자열 목록을 대입하는 방법
* Hash된 값과 원래 값을 Dictionary (사전) 데이터 베이스로 유지해놓고, Hash 값으로 원본 메시지를 검색할 수도 있음

### 방어 방법
* 가능하면 다중인증(Multi-factor authentication)을 설정
* 비밀번호 대신 생체 인식을 사용함
* 제한 시간 내에 허용되는 시도 횟수를 제한함
* 등등

## 13. 무차별 대입(Brute Force) 공격이란 무엇인가?
### 무차별 대입 공격이란?
*  특정한 암호를 풀기 위해 가능한 모든 값을 대입 방법
### 방어 방법
* 로그인 시도 횟수 제한
* 다중 인증
* 안전한 패스워드 규칙
* 솔트 값 추가(패스워드에 솔트 값을 추가한 후 해시함수를 적용하여 한 번 더 보안을 강화하는 방법)
* 등등


## 14. SQL 인젝션이란 무엇인가?
### SQL 인젝션이란?
*  클라이언트의 입력값을 조작하여 서버의 데이터베이스를 공격할 수 있는 공격방식

### 사용 방법?
* ex) 로그인 쿼리 : ```SELECT user FROM user_table WHERE id='세피로트' AND password='나무';```
* password에 ' OR '1' = '1 주입되면, ```SELECT user FROM user_table WHERE id='admin' AND password=' ' OR '1' = '1';``` 형태가 되면 password를 몰라도 해당 값이 true가 됨

### 방어 방법
* 기본적으로 유저에게 받은 값을 직접 SQL로 넘기면 안됨
* prepared statement 사용하기(SQL 쿼리를 사전에 컴파일한 뒤 변수만 따로 집어넣어 실행하는 것)


## 15. PreparedStatement가 어떻게 SQL 인젝션을 막을 수 있는지?
* Prepared Statement 구문을 사용하게 되면, 사용자의 입력 값이 데이터베이스의 파라미터로 들어가기 전에 DBMS가 미리 컴파일 하여 실행하지 않고 대기함
* 그 후 사용자의 입력 값을 문자열로 인식하게 하여 공격Query가 들어간다고 하더라도, 사용자의 입력은 이미 의미 없는 단순 문자열 이기 때문에 전체 Query문도 공격자의 의도대로 작동하지 않음
## 16. XSS, CSRF이란 무엇인가?
### XSS(Cross-Site Scripting)공격이란?
* XSS 공격은 크로스 사이트 스크립팅(Cross Site Scripting)을 뜻하며, 브라우저에서 특정 스크립트가 실행되도록 하는 공격 방식  
* 사용자의 쿠키나 세션의 정보를 획득하거나, 웹사이트를 변조하고, 피싱을 시도할 수 있음
* ex) 사이트의 게시판에 해커가 미리 만들어둔 악성 해킹 사이트로 이동하게끔 하는 스크립트를 삽입하고 게시글을 작성

### 방어 방법
* XSS 방어 라이브러리, 브라우저 확장 앱 사용
* 웹 방화벽 사용
* HttpOnly 옵션 활성화
  -  자바스크립트를 통해 쿠키 값에 접근하는 것을 막아줌
* XSS 특수문자 치환

### CSRF(Cross-Site Request Forgery) 공격이란?
* 현재 인증된 웹 애플리케이션에서 의도하지 않은 작업을 실행하도록 하는 공격  
* ex) 이메일 또는 채팅을 통한 해커의 링크 전송

### 방어 방법
* Referrer 검증
  -  해당 요청이 요청된 페이지의 정보를 확인하는 방법
* Security Token 사용 (A.K.A CSRF Token)
  - 서버에서 hash로 암호화 된 token을 발급, 사용자는 매 요청마다 token을 함께 보내어 서버의 검증을 받음


## 17. CORS란 무엇인가?

### SOP(Same Origin Policy)
* 웹 보안 정책으로 같은 출처에서만 리소스를 공유할 수 있다는 규칙을 가진 정책
* 출처는 URL의 Protocol, Host, Port로 구분

#### 왜?
* 클라이언트가 `http://abc.com`에 로그인 한 후 해커가 클라이언트에게 `http://hacker.ck`라는 URL로 접속하도록 유도
* 클라이언트가 해당 URL을 클릭하면 개인정보가 탈취됨
* SOP 정책으로 서로 다른 출처로 인해 해당 요청을 방지

### CORS(Cross Origin Resource Sharing)
* 추가 HTTP 헤더를 사용하여, 한 출처에서 실행 중인 웹 어플리케이션이 다른 출처의 선택한 자원에 접근할 수 있는 권한을 부여하도록 브라우저에게 알려주는 체제
* 즉, 다른 출처의 자원을 공유할 수 있는 규칙을 가진 정책

#### 왜?
* SOP 정책으로 인해 다른 도메인에 있는 리소스를 사용하지 못해 많은 불편함
* 따라서 예외적인 상황을 추가한 정책

#### CORS 접근제어 방식
* 단순 요청 (Simple Request) \
다른 출처의 리소스를 호출 할 때 request header에 Origin 헤더를 포함시켜서 전송 \
서버는 response header에 Access-Control-Allow-Origin 추가하여 값을 보내주고 \
브라우저는 해당 값을 보고 서버가 허용한 출처인지 판단

  - 조건
  1) GET, HEAD, POST 중의 한 가지 방식 사용
  2) POST 방식일 경우 Content-type 이 셋 중 하나
      - application/x-www-form-urlencoded
      - multipart/form-data
      - text/plain (default 설정)
  3) Custom header 를 전송하지 않을 것

  

* 사전 요청 (Preflight Request) \
  Simple Request 조건에 해당하지 않으면 브라우저는 Preflight Request 방식으로 요청 \
  먼저 OPTIONS 메서드를 통해 다른 도메인의 리소스로 HTTP 요청을 보내 실제 요청이 전송하기에 안전한지 확인

  - 조건
  1) GET, HEAD, POST 외의 다른 방식으로도 요청을 보낼 수 있음
  2) application/xml 처럼 다른 Content-type 으로 요청을 보낼 수 있음
  3) Custom header 사용 가능


* 인증 요청 (Credentialed Request)
  보안상의 이유로 쿠키를 요청으로 보낼 수 없도록 막고 있음 \
  자신을 인증해야 정상적인 응답을 받을 수 있는 상황에서 쿠키를 통한 인증이 필요할 경우 사용

  - 조건
  1) Credential 요청
      - 요청 시 XMLHttpRequest객체가 ```.withCredentials = true;```  해당 값을 갖음
      - 서버가 Access-Control-Allow-Credentials 헤더를 true로 설정하여 응답하면 정상적으로 처리
      - Access-Contorl-Allow-Credentials: true인 경우에는 반드시 Access-Control-Allow-Origin의 값이 하나의 origin 값으로 명시되어 있어야 정상적으로 동작

  2) Non-Credential 요청
      - 아무런 설정을 하지 않았을 경우 CORS 요청은 기본적으로 Non-Credential 요청

###  CORS Response 응답 Header 종류
* Access-Control-Allow-Origin
  - 단일 출처를 지정하여 브라우저가 해당 출처가 리소스에 접근하도록 허용. '\*'로 지정하는 경우 Origin 에 상관없이 모든 리소스에 접근하도록 허용함
* Access-Control-Allow-Headers
  - 실제 요청 시 사용할 수 있는 HTTP header 를 지정함
* Access-Control-Allow-Methods
  - 리소스에 접근할 때 허용되는 Method 를 지정함. 이 header 는 preflight request 에 대한 응답으로 사용됨
* Access-Control-Max-Age
  - preflight request 요청 결과를 캐시할 수 있는 시간(초 단위)을 지정함
* Access-Control-Allow-Credentials
  - credentials 플래그가 true 일 때, 요청에 대한 응답을 표시하기 위해 사용됨 이 header 를 설정하지 않을 경우, 브라우저가 응답을 무시하고 웹 컨텐츠로 반환되지 않음
* Access-Control-Expose-Headers
  - 브라우저가 접근할 수 있는 헤더를 서버의 화이트 리스트에 추가할 때 사용됨

###  CORS Request  Header 종류
* Access-Control-Request-Method
  - 실제 요청에서 사용하는 메서드를 서버가 알 수 있도록 설정하는 헤더
* Access-Control-Request-Headers
  - 실제 요청에 포함될 헤더를 서버가 알 수 있도록 설정하는 헤더
* Origin
  - 요청을 보낸 출처로, URL 중 scheme과 host, port만 명시

출처:https://developer.mozilla.org/ko/docs/Web/HTTP/CORS \
출처:https://velog.io/@logqwerty/CORS

## 18. JSESSIONID가 발급되는 과정을 개발자 도구를 통해 확인해보기

**1) 세션 테스트를 위한 간단한 서블릿 작성**
![image](https://user-images.githubusercontent.com/41093183/198872748-80470c4e-8ac1-4266-a21d-f3287f269116.png)
<br />
**2) 톰캣 실행 후 http://localhost:8080/session 호출**
<br />
**3) 첫 호출 후 상태 확인**
* Request Header
![image](https://user-images.githubusercontent.com/41093183/198872795-f784a3bb-acf2-431e-852e-572d7f3fbfdf.png)

* Response Header - Set-Cookie 헤더 확인
![image](https://user-images.githubusercontent.com/41093183/198872827-b0df0624-1c80-4128-8155-970c173ed1dc.png)

* Application탭에서 쿠키확인
![image](https://user-images.githubusercontent.com/41093183/198872855-bcb89b99-d53f-491b-88b6-9959a8cd839e.png)

<br />

**4) 두 번째 호출 이후**
* Request Header - JESSIONID 쿠키를 포함하여 요청
![image](https://user-images.githubusercontent.com/41093183/198872914-399a2ae2-b8db-4952-a239-db49933154e5.png)

* Response Header
![image](https://user-images.githubusercontent.com/41093183/198872953-74fc2fe1-cfc8-4560-831f-d7f721734fa2.png)

* Application탭에서 쿠키확인
![image](https://user-images.githubusercontent.com/41093183/198872975-0d9c9f59-75a6-43eb-b477-9300f79c80cd.png)


<br />

**5) 쿠키 삭제 이후 요청**
* 쿠키를 삭제하였기 때문에 Request헤더에 쿠키를 담지못하고 서버는 새로운 쿠키를 발급
![image](https://user-images.githubusercontent.com/41093183/198873366-779e866a-c49f-4659-8d3a-cae3e4fa6c8f.png)

## 목차
1. [HTTP 요청 헤더에는 어떤게 들어가는가?](#1-http-요청-헤더에는-어떤게-들어가는가)
3. [HTTP 응답 헤더에는 어떤게 들어가는가?](#2-http-응답-헤더에는-어떤게-들어가는가)
5. [HTTP 메서드는 어떤게 있고 각각 어떤 상황에 사용하는가? (주요 메서드들만)](#3-http-메서드는-어떤게-있고-각각-어떤-상황에-사용하는가-주요-메서드들만)
6. [HTTP 상태 코드는 어떤게 있고 각각 어떤 상황에 사용하는가? (주요 상태 코드들만)](#4-http-상태-코드는-어떤게-있고-각각-어떤-상황에-사용하는가-주요-상태-코드들만)
7. [HTTP 요청 바디에는 어떤게 들어가는가?](#5-http-요청-바디에는-어떤게-들어가는가)
8. [HTTP 응답 바디에는 어떤게 들어가는가?](#6-http-응답-바디에는-어떤게-들어가는가)
9. [프록시는 무엇인가?](#7-프록시는-무엇인가)
10. [클라이언트가 서버에게 파라미터를 보내는 방법들은 어떤게 있는가? 각각 어떤 상황에 사용하는가?](#8-클라이언트가-서버에게-파라미터를-보내는-방법들은-어떤게-있는가-각각-어떤-상황에-사용하는가)
11. [HTTP 메서드 중 '안전한' 메서드는 어떤걸 의미하는가?](#9-http-메서드-중-안전한-메서드는-어떤걸-의미하는가)
12. [HTTP 메서드 중 '멱등성 있는' 메서드는 어떤걸 의미하는가?](#10-http-메서드-중-멱등성-있는-메서드는-어떤걸-의미하는가)
13. [HTTP의 커넥션에 대해](#11-http의-커넥션에-대해)
14. [HTTP의 캐시에 대해](#12-http의-캐시에-대해)

## 1. HTTP 요청 헤더에는 어떤게 들어가는가?
**서버에게 클라이언트가 받고자 하는 데이터의 타입이 무엇인지와, 같은 부가정보를 제공**


* Accept : 서버에게 클라이언트가 자신의 요청에 대응하는 어떤 미디어 타입도 받아들일 것임을 의미, 클라이언트가 다룰 수 있는 MINE 타입이 열거됨
  - Accept-Language: 클라이언트가 다룰 수 있고 선호하는 언어 타입이 열거
  - Accept-Charset: 클라이언트가 다룰 수 있고 선호하는 문자 집합이 열거  ex) UTF8, BIG5, ISO-8859-2 등
  - Accept-Encoding: 클라이언트가 지원하는 Encoding 타입이 열거  ex) gzip, deflate 등
  - Accept: application/json, text/plain, \*/\* \
    (json > text > all type 순으로 받는다는 표현)
  - Accept-Language: en-US,en;q=0.5 \
    (언어는 en이라는 표현, q는 가중치)
  - Accept-Encoding: gzip, deflate, br
    (gzip, deflate, br(Brotli) 등등의 압축 포맷을 받는다는 표현)

* Host: 도메인 이름 , 요청하는 자의 호스트명, 포트 번호를 포함하고 있음  ex) Host: developer.mozilla.org

* Connection: Request 후 연결을 닫을 것인지 유지할 것인지를 나타냄  ex) Connection: Close , Connection: Keep-Alive

* User-Agent: Request가 만들어진 브라우저 타입을 알려줌, 요청자의 소프트웨어 정보를 표현(os, 브라우저, 기타 버전 정보)

* Content-Length: POST Request를 사용할 때, Request Body의 데이터 길이를 나타냄

* Content-Type: POST Request를 사용할 때, Request Body 데이터의 형식을 MIME 타입으로 나타냄

* cookie: 서버에 의해서 이전에 저장된 쿠키를 포함시키는 속성  ex) cookie: aaa=3LEMQRTO6EBF4; page_uid=bbb123p0YihsshvyCBRssssstWG-3033307; nx_ssl=100;

* Origin: POST같은 요청을 보낼 때, 요청이 어느 주소에서 시작되었는지를 나타내는데 이때 보낸 주소와 받는 주소가 다르면 CORS 문제가 발생하기도함

* AuthorizationAuthorization: 인증 토큰을 서버로 보낼 때 사용하는 헤더. API 요청같은 것을 할 때 토큰이 없으면 거절당하기 때문에 이 때, Authorization을 함.JWT(Json Web Token) 을 사용한 인증에서 주로 사용함

* If-Modified-Since: 페이지가 수정되었으면 최신 버전 페이지 요청을 위한 필드만일 요청한 파일이 이 필드에 지정된 시간 이후로 변경되지 않았다면, 서버로부터 데이터를 전송받지 않음

* Referer: 이 페이지를 요청한 이전 페이지가 무엇인지를 알려줌, 로그분석 시 유저의 자취를 분석하는데 유용함

출처: https://goddaehee.tistory.com/169 [갓대희의 작은공간:티스토리]

<br/>

## 2. HTTP 응답 헤더에는 어떤게 들어가는가?
**클라이언트에게 정보를 제공하기 위한 자신만의 헤더를 갖고 있음**

* date: 응답 메세지가 생성된 시간을 표현

* Location: Request 완료 또는 새 리소스 식별을 위해 요청된 URI가 아닌 위치로 Redirection하는데 사용

* Server: Request 처리를 위한 서버의 소프트웨어 정보가 들어감

* WWW-Authenticate: Request-URI에 적용될 수 있는 인증체계와 매개변수 정보가 들어감


* Allow: Request-URI에서 지원하는 Method가 열거됨


* Content-Encoding: Body에 포함된 컨텐츠의 인코딩 형태를 알려주는데 사용됨 ex) Content-Encoding: gzip


* Content-Type: 컨텐츠의 미디어 타입을 알려주는데 사용됨  ex) Content-Type: text/html; charset=ISO-8859-4


* Expires: 컨텐츠가 더 이상 유효하지 않을 수 있는 date/time을 제공하는데 사용함  ex) Expires: Fri, 16 Oct 2020 03:24:32 GMT


* Last-Modified: 리소스가 마지막으로 업데이트되었다고 여겨지는 date/time을 제공하는데 사용됨  ex) Last-Modified: Thu, 15 Oct 2020 14:47:59 GMT


* Accept-Ranges: 서버가 리소스 요청에 대한 수락 범위를 나타내는데 사용됨  ex) Accept-Ranges: bytes 


* ETag: 요청된 변형에 대한 엔티티 태그의 현재 값을 나타내는데 사용됨


* Content-Language: 컨텐츠에서 사용된 언어를 나타내는데 사용됨


* Content-Location: 메시지에 포함된 리소스의 위치를 공유하는데 사용됨


* Content-MD5: Body 컨텐츠의 MD5 코드를 제공하는데 사용됨


* Transfer-Encoding: 송수신자 간에 안전하게 전송하기 위해 메시지 본문에 적용된 변환 유형을 나타냄  ex) Transfer-Encoding: chunked

* Content-Security-Policy: 다른 외부 파일들을 불러오는 경우, 차단할 소스와 불러올 소스를 여기에 명시할 수 있음
  - Content-Security-Policy: default-src 'self' (자신의 도메인의 파일들만 가져올 수 있음)
  - Content-Security-Policy: default-src https: (https를 통해서만 파일을 가져올 수 있음)
  - Content-Security-Policy: default-src 'none' (못가져 오게 만듬)

* Access-Control-Allow-Origin: 요청 Host와 응답 Host가 다르면 CORS 에러가 발생하는데 서버에서 응답 메시지 Access-Control-Allow-Origin 헤더에 프론트 주소를 적어주면 에러가 발생하지 않음 ex) Access-Control-Allow-Origin: goddaehee.tistory.com
  - Access-Control-Request-Method : 실제로 보내려는 메서드
  - Access-Control-Request-Headers : 실제로 보내려는 헤더
  - Access-Control-Allow-Methods : 서버가 허용하는 메서드
  - Access-Control-Allow-Headers : 서버가 허용하는 헤더

출처: https://goddaehee.tistory.com/169 [갓대희의 작은공간:티스토리]

<br/>


## 3. HTTP 메서드는 어떤게 있고 각각 어떤 상황에 사용하는가? (주요 메서드들만)
* GET : 서버에서 클라이언트 지정한 리소스를 요청, 조회용

* PUT : 클라이언트에서 서버로 보낸 데이터를 지정한 이름의 리소스로 저장
  - 서버에 있는 리소스에 데이터를 입력하기위해 사용

* DELETE : 지정한 리소스를 서버에서 삭제 요청
  - 리소스를 삭제할 것을 요청, 그러나 보장하진 않음(HTTP 명세는 서버가 클라이언트에게 알지 않고 요청을 무시하는 것 허용)

* POST : 서버에 데이터를 보내기 위해 사용, 등록
  - 다양한 타입이 들어 갈 수 있기 때문에 HTTP 요청 헤더에 Content-type 필드를 명시해야 함 \
    ex) application/x-www-form-urlencoded, text/plain, multipart/form-data

* HEAD : 지정한 리소스에 대한 응답에서 , HTTP 헤더 부분만 요청
  - 리소스를 가져오지 않고도 그에 대해서 무엇인가를 알아낼수 있음(타입 등)
  - 응답의 상태 코드를 통해, 개체가 존재하는지 확인할 수 있음
  - 헤더를 확인하여 리소스가 변경되었는지 검사 가능


## 4. HTTP 상태 코드는 어떤게 있고 각각 어떤 상황에 사용하는가? (주요 상태 코드들만)

* 1xx (Informational): 정보성 상태 코드(요청이 수신되어 처리중)
  - 100 Continue: 요청자는 요청을 계속해야 함. 서버는 이 코드를 제공하여 요청의 첫 번째 부분을 받았으며 나머지를 기다리고 있음을 나타냄
  - 101 Switching Protocols: 요청자가 서버에 프로토콜 전환을 요청했으며 서버는 이를 승인하는 중 (websocket으로 Upgrade 될 때)

* 2xx (Successful): 성공 상태 코드(요청 정상 처리)
  - 200 OK : 요청 성공
  - 201 Created : 요청 성공해서 새로운 리소스가 생성됨
  - 202 Accepted : 요청이 접수되었으나 처리가 완료되지 않았음
  - 204 No Content : 서버가 요청을 성공적으로 수행했지만, 응답 페이로드 본문에 보낼 데이터가 없음

* 3xx (Redirection): 리다이렉션 상태 코드(요청을 완료하려면 추가 행동이 필요)
  - 301 Moved Permanently : 리다이렉트시 요청 메서드가 GET으로 변하고, 본문이 제거될 수 있음
  - 302 Found : 리다이렉트시 요청 메서드가 GET으로 변하고, 본문이 제거될 수 있음(임시적)
  - 303 See Other : 리다이렉트시 요청 메서드가 GET으로 변경
  - 304 Not Modified : 캐시를 목적으로 사용
  - 307 Temporary Redirect : 리다이렉트시 요청 메서드와 본문 유지(요청한 리소스가 Location 헤더에 주어진 URL 로 임시로 옮겨졌다는 것을 나타냄, 요청 메서드를 변경하면 안됨)
  - 308 Permanent Redirect : 리다이렉트시 요청 메서드와 본문 유지(요청 메서드를 변경하면 안됨)

* 4xx (Client Error): 클라이언트 에러 상태 코드(클라이언트 오류, 잘못된 문법등으로 서버가 요청을 수행할 수 없음)
  - 400 Bad Request : 클라이언트가 잘못된 요청을 해서 서버가 요청을 처리할 수 없음
  - 401 Unauthorized : 클라이언트가 해당 리소스에 대한 인증이 필요함
  - 403 Forbidden : 서버가 요청을 이해했지만 승인을 거부함
  - 404 Not Found : 요청 리소스를 찾을 수 없음
  - 405 Method Not Allowed: 요청에 지정된 방법을 사용할 수 없음

* 5xx (Server Error): 서버 에러 상태 코드(서버 오류, 서버가 정상 요청을 처리하지 못함)
  - 500 Internal Server Error : 서버 문제로 오류 발생, 애매하면 500 오류
  - 503 Service Unavailable : 서비스 이용 불가


출처: https://kyun2da.dev/CS/http-%EB%A9%94%EC%86%8C%EB%93%9C%EC%99%80-%EC%83%81%ED%83%9C%EC%BD%94%EB%93%9C/
출처: https://ko.wikipedia.org/wiki/HTTP_%EC%83%81%ED%83%9C_%EC%BD%94%EB%93%9C

<br/>

## 5. HTTP 요청 바디에는 어떤게 들어가는가?

* 전송되는 데이터가 들어감 (폼데이터 , 이미지, 바이너리 파일 등)
* 본문은 요청의 마지막 부분에 들어감, 모든 요청에 본문이 들어가지는 않음
* Content-type에 따라 바디 형태가 달라짐


    ex) \
    Content-type : application/json \
    ```{key: value}```


    Content-type : application/x-www-form-urlencoded \
    ```key=value&key=value```

    Content-type : mutipart/form-data 
    ```
    Content-Type: multipart/form-data;boundary="boundary"

    --boundary
    Content-Disposition: form-data; name="field1"

    value1
    --boundary
    Content-Disposition: form-data; name="field2"; filename="example.txt"

    value2
    --boundary--
    ```

## 6. HTTP 응답 바디에는 어떤게 들어가는가?
* 클라이언트가 요청한 리소스 데이터가 포함

## 7. 프록시는 무엇인가?
### Proxy란?
* 클라이언트와 서버 사이에 위치하여 그들 사이의 HTTP 메시지를 정리하는 중개인처럼 동작하는 서버

#### 특징
* 클라이언트 입장에서는 서버처럼 동작하고 서버 입장에서는 클라이언트처럼 동작

#### 사용이유
* 보안 : 프록시 서버를 사용함으로 서버의 IP를 숨길 수 있음, 따라서 외부의 직접 접근을 막을 수 있음
* 캐시: Proxy 서버 중 일부는 프록시 서버에 요청된 내용을 Cache함
* ACL : 사이트 접근에 대한 접근 정책을 정의할 수 있음 (ACL = Proxy Server에 접속할 수 있는 범위를 설정하는 옵션)
* Log/Audit : 회사 내 직원의 인터넷 사용을 레포팅하거나 반대로 인트라넷의 사용을 레포팅할 수도 있음
* 지역 네트워크의 제한 우회 : 프록시 서버를 사용하면 접속을 다른나라로 우회할 수 있게 됨

#### Proxy 종류

#### Forward Proxy
* 클라이언트와 원격 리소스 사이에 프록시 서버가 위치하는 것
* 사용자의 요청을 Forward Proxy가 대신 받아 요청

##### 활용
  - URL 필터링
  - 캐시저장

#### Reverse Proxy
* 애플리케이션 서버 앞에 Proxy 서버가 위치하는 것
* 클라이언트의 요청을 대신 받고, 서버의 응답을 받아 클라이언트에게 전달
* 보안을 위해 보통 기업의 네트워크 환경에서는 DMZ(내부 네트워크와 외부 네트워크 사이에 위치하는 구간) 라고 부르는 곳에 위치시키며, 요청을 받은 Reverse Proxy서버는 요청을 서버에게 넘겨줌
##### 활용
  - 로드밸런싱
  - 캐시
  - 보안정책




출처: https://engineer-mole.tistory.com/288 [매일 꾸준히, 더 깊이:티스토리] \
출처: https://nice-engineer.tistory.com/m/entry/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%82%B9-Proxy-%ED%94%84%EB%A1%9D%EC%8B%9C%EB%9E%80



## 8. 클라이언트가 서버에게 파라미터를 보내는 방법들은 어떤게 있는가? 각각 어떤 상황에 사용하는가?
### GET 방식 - 쿼리 스트링
* 입력한 데이터를 URL에 붙여서 전송, 데이터가 다 보이므로 보안에 취약함
* 전송할 수 있는 데이터는 256바이트를 넘을 수 없다.
* ex) 검색, 필터, 페이징등에서 많이 사용하는 방식


### POST 방식 - HTML Form
* 입력한 데이터를 본문안에 포함해서 전송
* 입력한 데이터가 URL에 보이지 않으므로 GET방식 보다 보안에 우수
* 전송할 데이터의 길이에 제한이 없음
* 복잡한 형태의 데이터를 전송할 때 유용함
* ex) 회원 가입, 상품 주문, HTML Form에 주로 사용

### HTTP API 방식
* HTTP message body에 데이터를 직접 담아서 요청
* 다양한 데이터 형식을 지원, 주로 JSON을 사용
* POST뿐만 아니라, PUT과 PATCH 형식으로도 사용할 수 있음

출처:https://velog.io/@woply/spring-HTTP-%EC%9A%94%EC%B2%AD-%EB%A9%94%EC%8B%9C%EC%A7%80%EB%A5%BC-%EC%9D%B4%EC%9A%A9%ED%95%B4-%EC%84%9C%EB%B2%84%EC%97%90-%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%A5%BC-%EC%A0%84%EB%8B%AC%ED%95%98%EB%8A%94-3%EA%B0%80%EC%A7%80-%EB%B0%A9%EB%B2%95

## 9. HTTP 메서드 중 '안전한' 메서드는 어떤걸 의미하는가?
### 안전한 메서드란?
* HTTP 요청의 결과로 서버에 상태를 바꾸지 않음

### 해당 메서드
* GET, HEAD, OPTIONS

### 사용이유
* 의도치않게 호출될 수 있는 경우가 많기때문임. 안전하지 않으면 예상치 못하게 호출했을 때 사이드이펙트가 생길수도 있음


## 10. HTTP 메서드 중 '멱등성 있는' 메서드는 어떤걸 의미하는가?

### 멱등성 있는 메서드란?
* 한 번 혹은 여러 번 실행됐는지에 상관없이 같은 결과를 반환한다면 그 트랜잭션은 멱등하다고 함

### 해당 메서드
* GET, HEAD, PUT, DELETE, TRACE, OPTIONS

#### PUT 메서드가 멱등인 이유
* 예를 들어 PUT /data/3 여러 번 요청 시 3번째 Data는 우리가 요청한 그 값으로 수정된 항상 같은 상태

### 사용이유
* 추가 부작용 없이 요청을 재전송하거나 재시도할 수 있음


출처:https://velog.io/@gidskql6671/HTTP-Method%EC%9D%98-%EB%A9%B1%EB%93%B1%EC%84%B1

## 11. HTTP의 커넥션에 대해
* HTTP 통신은 TCP/IP를 통해 이루어짐
* HTTP 트랜잭션의 성능은 그 아래 계층인 TCP 성능에 영향을 받음

### HTTP 트랜잭션 성능에 영향을 미치는 TCP 요소
#### TCP 커넥션의 핸드셰이크
- 새로운 TCP 커넥션이 생성될 때 생기는 지연
- 크기가 작은 HTTP 트랜잭션일 경우 전체 시간의 50% 이상의 TCP 구성하는데 사용



#### TCP의 slow start
- TCP 커넥션은 처음에는 최대 속도를 제한하고 데이터가 성공적으로 전송됨에 따라서 속도 제한을 높여나가는 것
- '튜닝'된 커넥션을 재사용하는 기능 - "지속 커넥션"




#### 데이터를 한데 모아 한 번에 전송하기 위한 네이글 알고리즘
- 보낼 수 있는 데이터를 바로 패킷으로 만들지 않고, 가능한 버퍼에 모아서 더 큰 패킷으로 만들어 한번에 보내는 방법
- 네트워크 비용은 절감하게 되지만, 대신 패킷 하나당 처리량이 늘어나므로 반응속도는 조금 느려질 수 있음




#### TCP의 편승 확인응답을 위한 확인응답 지연 알고리즘
- 각 세그먼트 수신자는, 세그먼트를 받으면 확인응답 패킷을 반환한다. 만일 반환이 없다면 패킷이 파기되었거나 오류가 있다고 판단해 재전송함
- 이 때 확인응답은 크기가 작기 때문에 같은 방향으로 보내야 할 데이터 패킷에, 확인 응답을 편승시키게 되는데 같은 방향으로 보내는 패킷이 많지않을 때 지연 발생 가능성이 있음




#### TIMT_WAIT 지연과 포트 고갈
- TIME_WAIT : TCP 커넥션이 끊기고 일정 시간 동안 같은 주소와 포트 번호를 사용하는 새로운 TCP 커넥션을 생성을 막기 위한 것
- 성능 테스트 시 하나의 클라이언트에서 하나의 서버로 테스트로 할 경우 약 60,000개의 포트를 다 사용하여 TIME_WAIT 포트 고갈이 일어날 수 있음


 


### HTTP 커넥션 최적화 기술

#### Keep Alive 커넥션 (HTTP 1.0+)
- 서버와 클라이언트가 맺은 연결을 유지하는 방식
- 기존 단기커넥션(connection 하나 당 1 Request & 1 response 처리)을 보완한 커넥션
- 사용 시 Connection:Keep-Alive 요청헤더를 보내야 함



#### 병렬(parallel) 커넥션 (HTTP 1.1)
- 여러 개의 TCP 커넥센을 통한 동시 HTTP 요청
- 다수의 커넥션은 메모리를 많이 소모하기 때문에 대부분 4개의 병렬 커넥션만을 허용
- 네트워크 대역폭이 좁을 때는 더 느릴 수 있음



#### 지속(persistent) 커넥션 (HTTP 1.1)
- 커넥션을 맺고 끊는 데서 발생하는 지연을 제거하기 위한 TCP 커넥션의 재활용
- 클라이언트나 서버가 커넥션을 끊기 전까지는 커넥션을 유지
- 커넥션을 맺기 위한 준비작업에 따르는 시간을 절약 할 수 있고, TCP의 느린 시작으로 인한 지연을 피할 수 있음
- 지속시간을 잘못 관리할 경우 서버에 수많은 커넥션이 쌓여서 불필요한 소모를 발생 시킬 수 있음
- HTTP/1.0+에 keep-alive 커넥션, HTTP/1.1에 '지속' 커넥션이 있음



#### 파이프라인(pipelined) 커넥션 (HTTP 1.1)
- 공유 TCP 커넥션을 통한 병렬 HTTP 요청
- 지속 커넥션을 통해서 요청을 파이프라이닝 할 수 있음(한 커넥션이 요청을 보내고 그 응답을 받기 전에 또 요청을 보낼 수 있음, 응답은 순차적으로 받아야함)
- 여러개의 HTTP Request 를 하나의 TCP/IP Packet 으로 연속적으로 Packing 해서 요청을 보냄(network latency 감소)



#### 다중(multiplexed) 커넥션 (HTTP 2.0)
    - HTTP/1.1의 PIPELINING의 개선으로 한 커넥션으로 동시에 여러 개의 메시지를 주고받을 수 있음, 요청 순서에 상관없이 먼저 완료된 순서대로 클라이언트에게 전달



  
출처:https://jwdeveloper.tistory.com/218 \
출처:https://bbo-blog.tistory.com/87?category=1004651

## 12. HTTP의 캐시에 대해
### HTTP 캐시
* HTTP 캐시는 이전에 가져온 리소스들을 재사용함으로써 성능 향상을 시킬 수 있음
* HTTP 헤더를 통해 브라우저의 캐싱 정책을 정할 수 있음

### HTTP 캐시 종류
![image](https://user-images.githubusercontent.com/41093183/196139455-a220680a-1145-4512-a299-7f4c68353b7e.png)

#### Private Cache
* 웹 브라우저에 저장되는 캐시이며, 다른 사람이 접근할 수 없음 단, 서버 응답에 Authorization 헤더가 포함되어 있다면 Private Cache에 저장되지 않음

#### Shared Cache
* Shared Cache 는 웹 브라우저와 서버 사이에서 동작하는 캐시를 의미하며, 다시 Proxy Cache와 Managed Cache 2가지로 나뉨

##### Shafred Cache 종류
* Proxy Cache
  - (포워드) 프록시에서 동작하는 캐시
* Managed Cache
  - AWS Cloudfront 혹은 Cloudflare 와 같은 CDN 서비스 그리고 리버스 프록시에서 동작하는 캐시, 이런 서비스들의 관리자 패널에서 직접 캐시에 대한 설정을 관리하거나 리버스 프록시 설정으로 관리할 수 있으므로 Managed Cache라고 불림

### 캐시 처리 단계
![image](https://user-images.githubusercontent.com/41093183/196132794-1f99085a-f435-46bc-96fb-7594971c4b17.png)

###  Cache-Control HTTP 헤더를 통해 캐싱 정책을 정의
* 요청과 응답 양측 모두에 있어 캐싱 메커니즘을 위한 디렉티브를 지정하는데 사용
* HTTP/1.1에서 추가됨 

     - Cache-Control: no-store
        + 클라이언트 요청 혹은 서버 응답에 관해서 어떤 것도 저장해서는 안됨
        + 브라우저가 캐싱을 하지 않고 매번 서버에게 요청
     - Cache-Control: no-cache
        + 리소스에 대한 캐시를 생성하지만, 리소스를 요청할 때 원 서버에 항상 캐시 유효성 검증을 하는 옵션
     - Cache-Control: must-revalidate
        + 캐시 만료 후 최초 조회시 원 서버에 검증해야함
        + 원 서버 접근 실패시 반드시 오류가 발생해야함 (504, Gateway Timeout)
     - Cache-Control: max-age=n
        + 캐시의 신선도를 초 단위로 설정 , Expires 헤더와 같이 쓰이면 Expires헤더는 무시됨
     - Cache-Control: public
        + 디렉티브를 사용하면 Shared Cache 에서도 캐싱을 허용
     - Cache-Control: private
        + 사용자 브라우저에게만 캐싱을 허용

### 캐시 유효성 검증 및 조건부 요청
#### 캐시 유효성 검증 및 조건부 요청 이란?
* 실제 원본 데이터가 수정 되었을 때만 리소스를 내려 받는 과정을 캐시 유효성 검증(validation) 및 조건부 요청(conditional request)이라고 함
* 유효성 검증 : 캐시의 유효 기간이 만료되었는지 확인
* 조건부 요청 : 리소스의 수정 유무에 따라 서버에게 리소스를 새로 받을 것인지, 기존에 캐시된 리소스를 그대로 제공할 지 결정하는 요청

#### 사용 이유
* 캐시의 유효 기간이 지난 다음 다시 서버에 리소스를 요청하면 이전과 다르지 않은 데이터를 그대로 받는경우 의미 없이 트래픽이 낭비가 됨
* 따라서 같은 데이터 변경이 없을 경우 기존 것 그대로 사용

#### 방법
- **Last-Modified** 와 **If-Modified-Since** 를 사용하는 방법
    * 리소스의 마지막 갱신 시각으로 검증하는 방법
    * 최초 요청 시 **서버**는 요청한 리소스가 마지막으로 수정된 일자를 나타내는 **Last-Modified 헤더를 응답**해줌
    * 두 번째 요청 시 브라우저는 **If-Modified-Since** 헤더에 전에 저장해둔 **Last-Modified를 설정하여 보내줌**
    * 서버는 **If-Modified-Since를 보고 리소스 수정 날짜와 비교하여 변경이 없었으면 304 응답코드를 그게아니면 리소스를 보내줌**
    * 밀리 세컨드 단위로 시각을 설정할 수 없다는 한계점이 존재
  
- **ETag** 와 **If-None-Match** 를 사용하는 방법
    * 리소스의 식별자를 기준으로 검증하는 방법
    * 최초 요청 시 **서버**는 **ETag 라는 응답 헤더**해줌
    * 두 번째 요청 시 브라우저는 **If-None-Match**라는 헤더에 저장해둔 **ETag 값을 설정하여 보내줌**
    * 서버는 **If-None-Match를 보고 리소스 수정이 되지 않았다면 304 응답코드를 그게아니면 리소스를 보내줌**

### 그 외 헤더들?
* Pragma : no-cache (HTTP 1.0하위호환까지 막아주려면 이 코드넣기)
* s-maxage : 중간 서버에서만 적용되는 max-age 값을 설정하기 위해 s-maxage 값을 사용할 수 있음
* Vary : 동일한 URL에 대해 요청을 하더라도 요청한 사용자의 특징(User Agent, Accept Encoding, Origin 등등)에 따라 서로 다른 응답을 해 주기 위해서 존재하는 헤더, 동일 URL이라 하더라도 다른 종류의 컨텐츠를 캐싱하고, 제공해야 함 

### CDN
#### CDN(Content Delivery Network) 이란?
* 지리적으로 분산된 여러 개의 서버로 웹 콘텐츠를 사용자와 가까운 곳에서 전송함으로써 전송 속도를 높이기위해 사용
* Content 캐시서버로 사용

#### CDN Invalidation란
* 클라이언트와 서버 사이에 효율을 높이기 위해 존재하는 CDN에서도 캐시를 할 수 있으며, CDN에 저장되어 있는 캐시를 삭제하는게 CDN Invalidation이라고함

### 휴리스틱 캐싱
* 브라우저는 Cache-Control이 없어도 휴리스틱 캐싱을 통해서 암묵적인 캐싱을 진행함
* 만약 응답에 Cache-Control: max-age나 Expires 둘 다 없다면 캐시는 경험적인(Heuristic) 방법으로 최대 나이를 계산
* 휴리스틱 신선도 유지기간은 보통 1주일, 보수적인 사이트의 경우 하루 정도의 상한이 설정됨

### 캐시 무효화(Cache Busting)
* 기본 캐시 키(primary cache key)는 요청 메서드와 URI로 구성
* 위의 특성을 이용하여 css, img 등을 장기간 캐시하여 효율을 높이고, 변경될 때 URL을 변경하여 즉시 갱신하게 하는 방법

#### 캐시 무효화 방법
* 파일명에 버전 포함하기 ex) bundle.v2.js
* 경로에 버전 포함하기 ex) /v2/bundle.js
* 파일명에 파일의 해시 포함하기 ex) bundle.ec0405c5aef93e771cd80e0db180b88b.js
* 쿼리 스트링에 버전 포함하기 ex) bundle.js?v=2
* 쿼리 스트링에 파일의 해시 포함하기 ex) bundle.js?v=ec0405c5aef93e771cd80e0db180b88b 
  - 쿼리 스트링을 사용할 경우 캐시를 아예 안하는 브라우저, 프록시, CDN이 있기 때문에 주의해야함

<br />

출처:https://thisblogfor.me/web/http/cache/ \
출처:https://toss.tech/article/smart-web-service-cache \
출처:https://velog.io/@tco0427/HTTP-%EC%BA%90%EC%8B%B1

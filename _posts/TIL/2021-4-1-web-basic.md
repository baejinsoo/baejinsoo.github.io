---
title: "Spring - WEB 기본지식 HTTP"
excerpt: "모든 개발자를 위한 HTTP 웹 기본 지식"
categories:
  - Spring
last_modified_at: 2021-04-01
toc: trues
toc_sticky: true
---

## WEB 기본지식

### TCP (Transmission Control Protocol)

> 연결지향 - TCP 3 way handshake

- 데이터 전달 보증
- 순서 보장
- 신뢰할 수 있는 프로토콜

![image](https://user-images.githubusercontent.com/17541671/113282146-820c9a80-9321-11eb-87ba-8a376e3e1aa4.png)

### REST (Representational State Transfer: 자원의 상태 전달)** 

1.  Client, Server: 클라이언트와 서버가 서로 독립적으로 분리 되어 있어야 한다.

2.  Stateless: 요청에 대해서 클라이언트의 상태를 서버에 저장하지 않는다.

3.  Cashe: 클라이언트는 서버의 응답을 Cashe(임시저장) 할 수 있어야 한다.

   클라이언트가 Cache를 통해서 응답을 재사용할 수 있어야 하며, 이를 통해서 서버의 부하를 낮춘다.

4. 계층화: 서버와 클라이언트 사이에, 방화벽, 게이트웨이, Proxy 등 다양한 계층 형태로 구성이 가능해야 하며, 이를 확장 할 수 있어야 한다.
5. Code on Demand (Optional): 자바 애플릿, 자바스크립트, 플래시 등 특정한 기능을 서버로부터 클라이언트가 전달받아 코드를 실행 할 수 있어야 한다.



#### REST Ful

1. 자원의 식별

   - 웹 기반의 REST에서는 리소스 접근을 할 때 URI를 사용한다.

     https://foo.co.kr/user/100

     Resource: user

     식별자: 100

2. 메시지를 통한 리소스 조작

   - Web에서든 다양한 방식으로 데이터를 전달 할 수 있다.(HTML, XML, JSON..)
   - 어떠한 타입의 데이터인지 알려주기 위해 HTTP Header 부분에 content-type을 통해서 데이터 타입을 지정해줌
   - 리소스 조작을 위해서 데이터 전체를 전달 하지 않고, 이를 메시지로 전달

3.  자기서술적 메시지

   - 요청 하는 데이터가 어떻게 처리 되어져야 하는지 충분한 데이터를 포함 해야 한다.
   - HTTP 기반의 REST에서는 HTTP Method와 Header 정보, 그리고 URI의 포함되는 정보로 표현 가능하다.
   - GET, POST, PUT, DELETE



### URI 설계 패턴

![image](https://user-images.githubusercontent.com/17541671/113282319-b7b18380-9321-11eb-9b7b-94504b847e0d.png)

- URI (Uniform Resource Identifier)

  Unifrom: 리소스 식별하는 통일된 방식

  Resource: 자원, URI로 식별할 수 있는 모든 것

  Identifier: 다른 항목과 구분하는데 필요한 정보

- URL (Uniform Resource Locator) - URI의 하위 개념

  인터넷 상에서의 자원, 특정 파일이 어디에 위차하는지 식별 하는 주소

- URN: 리소스에 이름을 부여

![image](https://user-images.githubusercontent.com/17541671/113282378-ca2bbd00-9321-11eb-81dc-787ed24cfe1e.png)



#### URI 설계 원칙 (RFC-3986)

- 슬래시 구분자(/) 는 계층 관계를 나타내는데 사용한다.

- URI 마지막 문자에는 (/)를 사용하지 않는다.

- 하이픈(-)은 URI 가독성을 높이는데 사용한다.

- 밑줄(_)은 사용하지 않는다.

- URI 경로에는 소문자가 적합하다.

- 파일 확장자는 URI에 포함하지 않는다.

- 프로그래밍 언어에 의존적인 확장자를 사용하지않는다.

- 구현에 의존적인 경로를 사용하지 않는다.

- 세션 ID를 포함하지 않는다.

- 프로그래밍 언어의 Method명을 이용하지 않는다.

- 명사에 단수형보다는 복수형을 사용해야 한다. 컬렉션에 대한 표현은 복수로 사용

- 컨트롤러 이름으로는 동사나 동사구를 사용한다.

- 경로 부분 중 변하는 부분은 유일한 값으로 대체한다.

- CRUD 기능을 나타내는 것은 URI에 사용하지 않는다.

- URI Query Parameter 디자인

  URI 쿼리 부분으로 컬렉션 결과에 대해서 필터링 할 수 있다.

  URI 쿼리는 컬렉션의 결과를 페이지로 구분하여 나타내는데 사용한다.

- API에 있어서 서브 도메인은 일관성 있게 사용해야 한다.
- 클라이언트 개발자 포탈 서브 도메인은 일관성 있게 만든다.



### HTTP Protocol

> HTTP (Hyper Text Transfer Protocol)로 RFC 2616에서 규정된 Web에서 데이터를 주고 받는 프로토콜

- TCP를 기반으로 REST의 특징을 모두 구현하고 있는 Web 기반의 프로토콜
- 메시지를 주고 (Request) 받는 (Response) 형태의 통신 방법
- 무상태 프로토콜(Stateless), 비연결성



#### HTTP 메서드의 속성

![image-20210401194339175](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210401194339175.png)



#### HTTP 상태코드

- 1xx (Informational): 요청이 수신되어 처리중

- 2xx (Successful): 요청 정상 처리

  - 200 OK
  - 201 Created: 요청 성공해서 새로운 리소스가 생성
  - 202 Acceptd : 요청이 접수되었으나 처리가 완료되지 않음
  - 204 No Content: 요청을 성공했으나, 응답 페이로드 본문에 보낼 데이터가 없음

- 3xx (Redirection): 요청을 완료하려면 추가 행동이 필요

  - 300 Multiple Choices
  - 301 Moved Permanently
  - 302 Found: GET으로 변할 수 있음
  - 303 See Other: 메서드가 GET으로 변경
  - 304 Not Modified: (캐시로 리다이렉트 한다.)
  - 307 Temporary Redirect: 메서드가 변하면 안됨
  - 308 Permanent Redirect

  307, 303을 권장하지만 현실적으로 이미 많은 애플리케이션 라이브러리들이 302를 기본값으로 사용

  자동 리다이렉션시에 GET으로 변해도 되면 그냥 302를 사용해도 큰 문제 없음

- 4xx (Client Error): 클라이언트 오류, 잘못된 문법등으로 서버가 요청을 수행할 수 없음- 요청을 다시 검토하고 보내야함.

  - 401 Unauthorized: 클라이언트가 해당 리소스에 대한 인증이 필요함
  - 403 Forbidden: 서버가 요청을 이해했지만 승인을 거부함
  - 404 Not Found: 요청 리소스를 찾을 수 없음

- 5xx (Server Error): 서버 오류, 서버가 정상 요청을 처리하지 못함 - 서버에 문제가 있기 때문에 재시도 하면 성공할 수도 있음

  - 500 Internal Server Error: 서버 문제로 오류 발생, 애매하면 500 오류
  - 503 Service Unavailable: 서비스 이용 불가(ex 과부하)



#### HTTP 헤더

```
HTTP/1.1 200 OK
Content-Type:text/html;charset=UTF-8
Content-Length:3423

<html>
	<body>...</body>
</html>
```

##### 용도

- HTTP 전송에 필요한 모든 부가정보

  예) 메시지 바디의 내용, 메시지 바디의 크기, 압축, 인증, 요청 클라이언트, 서버 정보, 캐시 관리 정보...



##### RFC723x 변화

- 엔티티 -> 표현(Representation)
- 표현 = 표현 메타데이터 + 표현 데이터



##### message body - RFC7230(최신)

- 메시지 본문(message body)를 통해 표현 데이터 전달
- 메시지 본문 = payload
- 표현은 요청이나 응답에서 전달할 실제 데이터
- 표현 헤더는 표현 데이터를 해석할 수 잇는 정보 제공
  - 데이터 유형(html, json), 데이터 길이, 압축 정보...



##### 쿠키

- Set-Cookie: 서버에서 클라이언트로 쿠키 전달(응답)

  예) set-cookie: sessionId=abc123;expire=Sat,26-Dec-2020 00:00:00 GMT; path=/;domain=.google.com;Secure

- Cookie: 클라이언트가 서버에서 받은 쿠키를 저장하고, HTTP 요청시 서버로 전달



사용처 - 사용자 로그인 세션 관리, 광고 정보 트래킹

쿠키 정보는 항상 서버에 전송됨

- 네트워크 트래픽 추가 유발
- 최소한의 정보만 사용(세션 id, 인증 토큰)
- 서버에 전송하지 않고, 웹 브라우저 내부에 데이터를 저장하고 싶으면 웹 스토리지(localStorage, sesseionStorage) 참고



#### 캐시

##### 캐시가 없을 때

- 데이터가 변경되지 않아도 계속 네트워크를 통해서 데이터를 다운받아야 한다.
- 인터넷 네트워크는 매우 느리고 비쌈
- 브라우저 로딩 속도가 느리다

##### 캐시 적용

- 캐시 가능 시간동안 네트워크 사용하지 않아도 된다.
- 비싼 네트워크 사용량을 줄일 수 있다.
- 브라우저 로딩 속도가 매우 빠르다.



##### 캐시 시간이 초과 했을 경우

###### 검증 헤더와 조건부 요청 1: Last-Modified, If-Modified-Since

- 캐시 유효 시간이 초과해도, 서버의 데이터가 갱신되지 않은경우

- 304 Not Modified + 헤더 메타 정보만 응답(바디X)

- 클라이언트는 서버가 보낸 응답 헤더 정보로 캐시의 메타 정보를 갱신

- 클라이언트는 캐시에 저장된 데이터 재활용

- 결과적으로 네트워크 다운로드가 발생하지만 용량이 적은 헤더 정보만 다운로드

  

###### 검증 헤더와 조건부 요청 2:  ETag, If-None-Match

ETag (Entity Tag): 캐시용 데이터에 임의의 고유한 버전 이름을 달아둠

- 데이터가 변경되면 이 이름을 바꾸어서 변경함(Hash를 다시 생성)

- ETag만 서버에 보내서 같으면 유지, 다르면 다시 받기
- 캐시 제어 로직을 서버에서 완전히 관리
- 클라이언트는 단순히 이 값을 서버에 제공



##### 프록시 캐시

![image](https://user-images.githubusercontent.com/17541671/113307982-ac218500-9340-11eb-8f53-2895bdaf841f.png)

![image](https://user-images.githubusercontent.com/17541671/113308032-b80d4700-9340-11eb-8bb3-124c4f4132e6.png)



##### 캐시 무효화

Cache-Control: no-cache, no-store, must-revalidate

- no-cache: 데이터는 캐시해도 되지만, 항상 원 서버에 검증하고 사용

- no-store: 데이터에 민감한 정보가 있으므로 저장하면 안됨- 메모리에서 사용하고 최대한 빨리 삭제

- must-revalidate: 캐시 만료후 최초 조회시 원 서버에 검증해야함.

  ​	원 서버 접근 실패시 반드시 오류발생(504)

  ​	
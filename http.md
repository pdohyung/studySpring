인터넷 네트워크
---
* 인터넷 통신
* IP(Internet Protocol)
* TCP(3 way handshake), UDP
* PORT
* DNS

URI (Uniform Resource Identifier)
---
* URI 위치는 변할 수 있지만, 이름은 변하지 않는다.
  + URL (Uniform Resource Locator) : 리소스가 있는 위치를 지정
  + URN (Uniform Resource Name) : 리소스에 이름을 부여

HTTP (HypeText Transfer Protocol)
---
* HTTP 특징
  - 클라이언트 서버 구조 : Request Response 구조, 클라이언트는 서버에 요청을 보내고 응답을 대기한다.
  - 무상태 프로토콜 (Stateless) : 서버가 클라이언트의 상태를 보존하지 않는다. 서버 확장성이 높지만 클라이언트가 추가 데이터를 전송해야한다.
  - 비연결성 (connectionless) : HTTP는 기본적으로 비연결성 모델 동시에 처리할 요청은 적기 때문에 서버 자원을 매우 효율적으로 활용 가능하다.
  - HTTP 메세지에 모든 것을 전송, HTTP 메세지 , 단순함 확장 가능

HTTP 메서드
---
  * HTTP API를 설계할 때 가장 중요한 것은 리소스 식별이다. 행위를 배제하고 리소스를 URI에 매핑한다.
    - GET : 리소스 조회, 서버에 전달할 때는 query를 통해서 전달
    - POST : 요청 데이터 처리 및 주로 등록에 사용, 메세지 바디를 통해 서버로 요청 데이터 전달 
    - PUT : 리소스가 있으면 대체, 해당 리소스가 없으면 생성 
    - PATCH : 리소스 부분 변경
    - DELETE : 리소스 삭제
  * HTTP 메서드의 속성
    - 안전 (Safe Methods) : 호출해도 리소스를 변경하지 않는다. ex) GET
    - 멱등 (Idempotent Methods) : 한 번 호출하던 여러번 호출하던 같은 결과가 조회된다. POST는 멱등이 아니다.
    - 캐시가능 (Cacheable Methods) : 응답 결과 리소스를 캐시해서 사용해도 되는가 ? GET, HEAD, POST, PATCH 캐시 가능

HTTP API, FORM
---
    * 문서 (document) : 단일 개념 (파일 하나, 객체 인스턴스, 데이터베이스 row) ex) members/100, /file/star.jpg
    * 컬렉션 : POST 기반 등록, 서버가 리소스 URI 생성하고 관리, 서버가 관리하는 리소스 디렉터리 ex) members
    * 스토어 : PUT 기반 등록, 클라이언트가 리소스 URI를 알고 관리, 클라이언트가 관리하는 자원 저장소 ex) files
    * FORM : 순서 html + html FORM 사용 GET, POST만 지원
    * 컨트롤러, 컨트롤 URI : 문서, 컬렉션, 스토어로 해결하기 어려운 추가 프로세서 실행, 동사를 직접 사용, ex) /members/{id}/delete

HTTP 상태코드
---

클라이언트가 보낸 요청의 처리 상태를 응답에서 알려주는 기능
  * 1xx (Informational) : 요청이 수신되어 처리중
  * 2xx (Successful) : 요청 정상 처리
  * 3xx (Redirection) : 요청을 완료하려면 추가 행동이 필요
    - 영구 리다이렉션 : 특정 리소스의 URI가 영구적으로 이동 ex) /members -> /users , /event -> /new-event
    - 일시 리다이렉션 : 일시적인 변경 ex) 주문 완료 후 주문 내역 화면으로 이동, PRG (Post/Redirect/Get)
    - 특수 리다이렉션 : 결과 대신 캐시를 사용
  * 4xx (Client Error) : 클라이언트의 요청에 잘못된 문법등으로 서버가 요청을 수행할 수 없음, 클라이언트가 이미 잘못된 요청, 데이터를 보내고 있기 때문에, 똑같은 재시도가 실패함
  * 5xx (Server Error) : 서버 내부 문제로 오류 발생, 애매하면 500 오류
 
 HTTP 일반 헤더
 ---
 
  * 용도
    - HTTP 전송에 필요한 모든 부가 정보
    - ex) 메세디 바디의 내용, 메세지 바디의 크기, 압축, 인증, 요청 클라이언트, 서버 정보, 캐시 관리 정보
  * 헤더 분류
    - General 헤더 : 메세지 전체에 적용되는 정보, ex) Connetion: close
    - Request 헤더 : 요청 정보, ex) User-Agent: Mozilla / 5.0
    - Respoonse 헤더 : 응답 정보, ex) Server: Apache
    - Entity 헤더 : 엔티티 바디 정보, ex) Content-Type: text/html, Content-Length: 3423
  * HTTP BODY
    - 메세지 본문(message body)을 통해 표현 데이터 전달
    - 메세지 본문 = 페이로드(payload)
    - 표현은 요청이나 응답에서 전달할 실제 데이터
    - 표현 헤더는 표현 데이터를 해석할 수 있는 정보 제공, ex) 데이터 유형(html, json), 데이터 길이, 압축 정보 등
  * 표현
    - Content-Type : 표현 데이터의 형식, 미디어 타입, 문자 인코딩
    - Content-Encoding : 표현 데이터의 압축 방식, 표현 데이터를 압축하기 위해 사용
    - Content-Language : 표현 데이터의 자연 언어, ex) ko, en, en-US
    - Content-Length : 표현 데이터의 길이, 바이트 단위
  * 협상
    - Accept : 클라이언트가 선호하는 미디어 타입 전달
    - Accept-Charset : 클라이언트가 선호하는 문자 인코딩
    - Accept-Encoding : 클라이언트가 선호하는 압축 인코딩
    - Accept-Language : 클라이언트 선호하는 자연 언어
  * 협상과 우선순위
    - Accept-Language : ko-KR, ko; q=0.9, en-US; q=0.8, en; q=0.7 , 0 ~ 1 클수록 우선순위
    - Accpet : text/*, text/plain, text/plain; format=flowed, */* 구체적인 것이 우선이다.
    - Accept : text/*, q=0.3, text/html; q=0.7, text/html; level=1, text/html; level=2; q=0.4, */*; q=0.5 구체적인 것을 기준으로 미디어 타입을 맞춘다.
  * 전송 방식
    - 단순 전송
    - 압축 전송
    - 분할 전송
    - 범위 전송
  * 일반 정보
    - From : 유저 에이전트의 이메일 정보, 요청에서 사용, 검색 엔진에서 주로 사용
    - Referer : 이전 웹 페이지 주소, 요청에서 사용, 유입 경로 분석 가능
    - User-Agent : 유저 에이전트 애플리케이션 정보, 요청에서 사용, 클라이언트의 애플리케이션 정보
    - Server : 요청을 처리하는 오리진 서버의 소프트웨어 정보, 응답에서 사용
    - Date : 메세지가 생성된 날짜, 응답에서 사용
  * 특별한 정보
    - Host : 요청한 호스트 정보 (도메인), 요청에서 사용, 필수
    - Location :  페이지 리다이렉션, 3xx 응답의 결과에 Loaction 헤더가 있으면 그 위치로 자동 이동
    - Allow : 허용 가능한 HTTP 메서드, GET, HEAD, PUT, 405(Method Not Allowed)에서 응답에 포함해야함
    - Retry-After : 유전 에이전트가 다음 요청을 하기까지 기다려야 하는 시간, 503(Service Unavailable) : 서비스가 언제까지 불능인지 알려줄 수 있음
      날짜 표기, 초단위 표기
  * 인증
    - Authorization : 클라이언트 인증 정보를 서버에 전달, Authorization : Basic xxxxxxxxxxxxxxx
    - WWW-Authenticate : 리소스 접근시 필요한 인증 정보 정의, 401 Unauthorized 응답과 함께 사용, WWW-Authenticate : Newauth realm = "apps", type = 1, title = "Login to             \"apps\"", Basic realm = "simple"
  * 쿠키
    - Set-Cookie : 서버에서 클라이언트에 쿠기 전달(응답), ex) set-cookie: sessionId = abcde1234; expires = Sat, 26-Dec-2020 00:00:00 GMT; path=\; domain =.google.com; Secure
    - Cookie : 클라이언트가 서버에서 받은 쿠키를 저장하고, HTTP 요청시 서버로 전달
    - 사용처 : 사용자 로그인 세션 관리, 광고 정보 트래킹
    - 쿠키 정보는 항상 서버에 전송됨, 네트워크 트래픽 추가 유발, 최소한의 정보만 사용 (세션 id, 인증 토큰), 서버에 전송하지 않고, 웹 브라우저 내부에 데이터를 저장하고 싶으면 웹 스토리지 참고
    - 보안에 민감한 데이터는 저장하면 안됨
  * 쿠키의 생명주기
    - 쿠키의 생명 주기는 날짜와 초로 설정 가능, 세션 쿠키 : 만료 날짜 생략하면 브라우저 종료시 까지만 유지, 영속 쿠키 : 만료 날짜를 입력하면 해당 날짜까지 유지
    - 도메인 : domain = example.org를 지정해서 쿠키 생성 dev.example.org도 쿠키 접근, 생략하면 example.org 에서 쿠키를 생성하고 domain 지정을 생략 dev.example.org는 쿠키 접근 X
  * 쿠키의 경로
    - ex) path=/home 이 경로를 포함한 하위 경로 페이지만 쿠키 접근, 일반적으로 path=/ 루트로 지정
  * 쿠키의 보안
    - Secure : 쿠키는 http, https를 구분하지 않고 전송, Secure를 적용하면 https인 경우에만 전송
    - HttpOnly : XSS 공격 방지, 자바스크립트에서 전송 불가, HTTP 전송에만 사용
    - SameSite : XSRF 공격 방지, 요청 도메인과 쿠키에 설정된 도메인이 같은 경우만 쿠키 전송
 

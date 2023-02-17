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
    - 문서 (document) : 단일 개념 (파일 하나, 객체 인스턴스, 데이터베이스 row) ex) members/100, /file/star.jpg
    - 컬렉션 : POST 기반 등록, 서버가 리소스 URI 생성하고 관리, 서버가 관리하는 리소스 디렉터리 ex) members
    - 스토어 : PUT 기반 등록, 클라이언트가 리소스 URI를 알고 관리, 클라이언트가 관리하는 자원 저장소 ex) files
    - FORM : 순서 html + html FORM 사용 GET, POST만 지원
    - 컨트롤러, 컨트롤 URI : 문서, 컬렉션, 스토어로 해결하기 어려운 추가 프로세서 실행, 동사를 직접 사용, ex) /members/{id}/delete


  


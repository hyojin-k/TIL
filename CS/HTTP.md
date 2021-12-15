# HTTP

## HTTP 프로토콜
- Hyper Text Transfer Protocol
- 웹에서 브라우저와 서버 간에 데이터를 주고받을 수 있는 통신을 하기 위한 프로토콜(규약)
- 초기에는 HTML과 같은 하이퍼미디어 문서를 주로 전송했지만, Plain text, JSON, XML 등 다양한 형태의 정보도 전송
- 상태가 없는(stateless) 프로토콜로, 데이터를 주고 받기 위한 각각의 데이터 요청이 서로 독립적이기 때문에, 서버는 세션과 같은 별도의 추가 정보를 관리하지 않아도 되고, 다수의 요청 처리 및 서버의 부하를 줄일 수 있는 이점이 존재 
=> 상태를 유지하기 위해 Cookie와 Session을 사용
- TCP/IP 통신 위에서 동작하는 응용 프로토콜(application protocol)
- 기본포트 : 80번

### HTTP Request(요청) / Response(응답)
- 클라이언트/브라우저(Client), 서버(Server)
    - 브라우저 => 서버 : Request(요청)
    - 서버 => 브라우저 : Response(응답)

### HTTP 요청 메서드 (Request Methods)
- 서버에 요청을 전송하기 위해 브라우저는 주소창을 제공하고, URL을 이용하여 서버에 특정 데이터 요청 가능 
- 주요 메서드
    - GET : 요청
    - POST : 생성
    - PUT : 변경
    - DELETE : 삭제
- 기타 요청 메서드
    - HEAD : 서버 헤더 정보 획득. GET과 비슷하지만 Response Body를 반환하지 않음
    - OPTIONS : 서버 옵션들을 확인하기 위한 요청. CORS에서 사용

### HTTP 상태 코드 (Status Code)
- 서버에서 설정해주는 응답 정보
- 상태코드를 통해 에러 처리 가능
- 주요 상태코드
    - 200번대 : 성공
    - 300번대 : 리다이렉션
    - 400번대 : 클라이언트 에러
        - 400 : Bad Request, 잘못된 요청
        - 401 : Unauthorized, 권한 없이 요청. Authorization 헤더가 잘못된 경우
        - 403 : Forbidden, 서버에서 해당 자원에 대해 접근 금지
        - 404 : 요청한 자원이 서버에 없음
        - 405 : Method Not Allowed, 허용되지 않은 요청 메서드
        - 409 : Conflict, 최신 자원이 아닌데 업데이트 하는 경우
    - 500번대 : 서버 에러

---

## HTTP/1.1 vs HTTP/2

### HTTP/1.1
- 기본적으로 커넥션당 하나의 요청과 응답만 처리
- HTML 문서 내에 포함된 여러 개의 리소스 요청(link, img, script ...)과 응답이 개별적, 순차적으로 전송
- 동시 전송이 불가능한 구조때문에 요청할 리소스 개수에 비례하여 대시 시간(Latency)도 증가

#### HTTP/1.1의 단점
1. HOL(Head Of Line) Blocking
- HTTP/1.1의 pipelining 기법을 사용하여 하나의 커넥션으로 다수의 파일을 요청/응답 할 수 있지만, 순차적으로 요청/응답이 진행되기 때문에 앞 순서에서 응답이 지연되면 처리되기 전까지 다음 순서의 응답은 대기해야하는 문제점 발생

2. RTT(Round Trip Time 왕복시간) 증가
- 3-way Handshake가 반복적으로 일어나고, 불필요한 RTT증가와 네트워크 지연을 초래하여 성능 저하
- 3-way Handshake란?
    - TCP/IP 프로토콜을 이용해서 통신을 하는 응용프로그램이 데이터를 전송하기 전에 정확한 전송을 보장하기 위해 상대방 컴퓨터와 사전에 세션을 수립하는 과정
    - TCP 접속을 성공적으로 성립하기 위해 반드시 필요

3. 무거운 Header 구조
- 사용자가 웹페이지에 방문할때마다 http 요청이 발생하면서 중복된 헤더값을 전송하게 되고, 해당 domain에 설정된 cookie 정보도 매 요청시 마다 헤더에 포함되어 전송되기 때문에 요청을 통해 전송되는 값보다 헤더 값이 더 큰 경우가 발생

### HTTP/2
- 커넥션당 동시에 여러 개의 요청과 응답이 가능
- 여러 리소스의 동시 전송이 가능하여 HTTP 1.1에 비해 페이지 로드속도가 약 50% 빠름

#### Multiplexed Streams
- 한 커넥션으로 동시에 여러개의 메세지를 주고 받을 수 있으며, 응답은 순서에 상관없이 stream으로 주고 받는다

#### Stream Prioritization
- 여러개의 파일을 클라이언트에서 요청했을 때 그 중 일부분의 렌더링이 늦어지는 문제가 발생하면, 리소스 간의 우선순위를 설정하여 문제를 해결

#### Server Push
- 클라이언트가 요청하지 않은 리소스를 Push 해주는 기법으로 클라이언트의 요청을 최소화해서 성능을 향상시킨다
- 클라이언트가 HTML 문서를 요청했고 그 안에 여러개의 리소스가 포함되어 있는 경우, HTTP/1.1에서는  필요한 리소스를 재요청하지만, HTTP/2에서는 서버가 알아서 포함된 리소스를 보내준다
- 이를 PUSH_PROMISE 라고 부르며, 이를 통해 서버가 전송한 리소스에 대해서는 클라이언트가 요청을 하지 않는다

#### Header Compression
- Header 정보를 압축하기 위해 Header Table 과 Huffman Encoding 기법 사용 => HPACK 압축방식
- 클라이언트가 두 번의 요청을 보내면 Header에 중복값이 존재하는 경우 static/dynamic Header Table 개념을 사용하여 중복된 Header는 index값만 전송하고, 중복되지 않은 Header 정보 값은 Huffman Encoding 기법으로 인코딩 처리하여 전송

#### 참고
[프런트엔드 개발자가 알아야하는 HTTP 프로토콜 Part 1](https://joshua1988.github.io/web-development/http-part1/)
[나만 모르고 있던 http2](https://www.popit.kr/%EB%82%98%EB%A7%8C-%EB%AA%A8%EB%A5%B4%EA%B3%A0-%EC%9E%88%EB%8D%98-http2/)
모던 자바스크립트 Deep Dive
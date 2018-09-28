
## URL과 리소스
### URI (Uniform Resource Identifier)
- 서버 리소스 이름은 통합 자원 식별자, 혹은 URI로 불린다.
- URI에는 두 가지가 있는데, URL과 URN이다. (URI = URL + URN)

### URL (Uniform Resource Locator)
- URL은 특정 서버의 한 리소스에 대한 구체적인 위치를 서술한다. (절대경로)
- 대부분 URL은 세 부분으로 이루어졌다.
  - 스킴(프로토콜) ex) http://
  - 호스트(주소) ex) www.simjunbo.com
  - 리소스(경로) ex) /user/simjunbo.gif

### URL 문법 (해당 문법을 다 쓰는 경우는 거의 없고 스킴, 호스트, 경로가 가장 중요하다)
- <스킴>://<사용자이름>:<비밀번호>@<호스트>:<포트>/<경로>;<파라미터>?<질의>#<프래그먼트>

### URI와 URL의 차이
- 고유의 식별자가 있으면 URI이다.
  - http://simjunbo.com/good.html (URI 이면서 URL)
  - http://simjunbo.com/user/132 (URI)
  
### URN (Unofirm Resource Name)
- 리소스의 위치에 영향 받지 않는 유일무이한 이름

### URL 인코딩 체계
- URL에 있는 안전하지 않은 문자들을 표현할 수 있는 인코딩 방식이 고안되었다.
- 예약어 : %, /, ., .., #, ?, ;, : 등

### URL의 단점
- URL은 주소이지 실제 이름이 아니다. 리소스가 옮겨지면 URL을 더는 사용할 수 없다.
- URN은 URL의 단점을 보완해서 위치와 상관 없이, 그 객체를 가리키는 실제 객체의 이름을 사용하는 것이다.


## HTTP 메시지
### 메시지
- 웹 클라이언트에서 웹 서버로 보낸 HTTP 메시지를 요청 메시지라고 부른다.
- 서버에서 클라이언트로 가는 메시지는 응답 메시지라고 부른다.
- HTTP 메시지는 세 부분으로 이루어진다.
  - 시작줄 : 요청이라면 무엇을 해야 하는지 응답이라면 무슨 일이 일어났는지
  - 헤더 : key : value 형태로 되어 있고 빈 줄로 끝난다. (헤더나 본문이 없더라도 HTTP 헤더의 집합은 항상 빈줄(CRLF)로 끝난다)
  - 본문 : 본문은 임의의 이진 데이터를 포함할 수 있다. 물론 텍스트도 가능
  
![http1](https://user-images.githubusercontent.com/7076334/46148825-e1e2e000-c2a3-11e8-9113-38c6490a7f44.gif)
  
### 시작줄
- 요청줄(요청 메시지의 시작줄) : 서버에서 어떤 동작이 일어나야 하는지 설명해주는 메서드와 그 동작에 대한 URL, HTTP 버전등 포함. 필드는 모두 공백으로 구분된다. ex) GET /simjunbo/memo.text HTTP/1.1
- 응답줄(응답 메시지의 시작줄) : HTTP의 버전, 상태 코드, 수행 상태에 대한 설명. 필드는 모두 공백으로 구분된다. ex) HTTP/1.0 200 OK

### 헤 더
- HTTP 헤더 필드는 요청과 응답 메시지에 추가 정보를 더한다. (기본적으로 이름/값 쌍의 목록)
- 일반 헤더 : 요청과 응답 양쪽에 모두 나타날 수 있음
- 요청 헤더 : 요청에 대한 부가 정보 제공
- 응답 헤더 : 응답에 대한 부가 정보 제공
- Entity 헤더 : 본문 크기와 콘텐츠, 혹은 리소스 그 자체를 서술
- 확장 헤더 : 명세에 정의되지 않은 새로운 헤더

### 엔티티 본문
- HTTP 메시지는 이미지, 비디오, HTML 문서, 소프트웨어 애플리케이션, 전자우편 등 여러 종류의 디지털 데이터를 실어 나를 수 있다.

### 메시지 본문
- 메시지 본문이 있는 경우 : POST, PUT
- 메시지 본문이 없는 경우 : GET, HEAD, TRACE, OPTIONS, DELETE

### 메서드(HEAD)
- 서버는 응답으로 헤더만을 돌려준다. 엔티티 본문은 결코 반환되지 않는다.
- 응답의 상태 코드를 통해, 개체가 존재하는지 확인할 수 있다.
- 헤더를 확인하여 리소스의 변경 여부를 확인할 수 있다.

### 메서드(TRACE)
- TRACE는 주로 진단을 위해 사용된다. ex) 요청이 의도한 요청/응답 연쇄를 거쳐가는지 검사할 수 있다. (Via)

### TRACE를 이용한 XST 공격
- XST 공격이란 기본적으로 HTTP 메서드 중 하나인 TRACE 메서드를 이용한 XSS 기법중 하나다.
- 클라이언트가 서버로 TRACE 요청을 후, 응답을 받을 때 반환되는 사용자의 쿠키정보등과 같은 중요 정보를 가로채는 공격이다.
- HTTP 메소드에서 TRACE를 제한하면 된다. 

### 메서드(OPTIONS)
- 웹 서버에게 여러 가지 종류에 대한 지원 범위를 물어볼 수 있다. ex) 특정 리소스에 대해 어떤 메서드가 지원되는가?

### 상태코드
- 100-199 : 정보성 상태코드
- 200-299 : 성공 상태 코드
- 300-399 : 리다이렉션 상태 코드
- 400-499 : 클라이언트 에러 상태 코드
- 500-599 : 서버 에러 상태 코드


## 커넥션 관리
### TCP
- TCP는 다음을 제공한다. (UDP 반대)
  - 오류 없는 데이터 전송
  - 순서에 맞는 전달
  - 조각나지 않는 데이터 스트림

### 계층별 데이터 종류
![default](https://user-images.githubusercontent.com/7076334/46154473-368c5800-c2b0-11e8-83b6-7a55c317f583.png)

### TCP 커넥션 핸드셰이크
![23594b4058723fb704](https://user-images.githubusercontent.com/7076334/46154935-232dbc80-c2b1-11e8-91d9-418ac1167bcd.gif)
  - 클라이언트는 새로운 TCP 커넥션을 생성하기 위해 작은 TCP 패킷을 서버로 보낸다. 그 패킷은 'SYN' 는 커낵션 생성 요청 플래그를 갖는다.
  - 서버에서 그 커넥션을 받으면 커넥션 요청이 받아들여졌음을 의미하는 'SYN'과 'ACK' 플래그를 포함한 TCP 패킷을 클라이언트에게 보낸다.
  - 마지막으로 클라잉언트는 커넥션이 잘 맺어졌음을 알리기 위해서 서버에게 다시 확인응답 신호 'ACK'를 보낸다.

### Keep-Alive 커넥션
- 커넥션을 맺고 끊는데 필요한 작업이 없어서 시간이 단축된다.
- HTTP/1.1 명세에서는 사용하지 않기로 결정해서 빠졌다.
- HTTP/1.1 에서는 대신, 설계가 더 개선된 지속 커넥션을 지원한다.

### 프로토콜 버전
- HTTP/0.9 : HTTP/0.9는 오직 GET 메서드만 지원하고, MIME타입이나, HTTP 헤더, 버전 번호는 지원하지 않는다. 금방 HTTP/1.0으로 대체되었다.
- HTTP/1.0 : 처음으로 널리 쓰이기 시작한 HTTP 버전이다. HTTP 헤더, 추가 메서드, 멀티미디어 객체 처리를 추가했다.
- HTTP/1.0+ : 오래 지속되는 'keep-alive', 가상 호스팅 지원, 프락시 연결 지원
- HTTP/1.1 : HTTP 설계의 구조적 결함 교정, 두드러진 서은ㅇ 최적화, 잘못된 기능 제거. (현재의 HTTP 버전)
- HTTP/2.0 : HTTP/1.1 성능 문제를 개선하기 위해 구글이 SPDY 프로토콜 기반으로 설계

## 웹서버

### 웹서버가 하는 일
- 1) 커넥션을 맺는다 : 클라이언트의 접속을 받아들이거나, 원치 않는 클라이언트는 다는다
- 2) 요청을 받는다 : HTTP 요청 메시지를 네트워크로부터 읽어 들인다.
- 3) 요청을 처리한다 : 요청 메시지를 해석하고 행동을 취한다.
- 4) 리소스에 접근한다 : 메시지에서 지정한 리소스에 접근한다.
- 5) 응답을 만든다 : 올바른 헤더를 포함한 HTTP 응답 메시지를 생성한다.
- 6) 응답을 보낸다 : 응답을 클라이언트에게 돌려준다.
- 7) 트랜잭션을 로그로 남긴다 : 로그파일에 트랜잭션 완료에 대한 기록을 남긴다.

### 웹의 구성요소
- 프록시 : 클라이언트와 서버 사이에 위치한 HTTP 중개자
- 캐시 : 많이 찾는 웹페이지를 클라이언트 가까이 보관하는 창고
- 게이트웨이 : 다른 애플리케이션과 연결된 특별한 웹 서버
- 터널 : 단순히 HTTP 통신을 전달하기만 하는 특별한 프록시

## 프록시
### 프록시
- 보안을 개선하고, 성능을 높여주며, 비용을 절약한다.
- 프록시 서버는 모든 HTTP 트래픽을 들여다보고 건드릴 수 있기 때문에, 트래픽을 감시하고 수정할 수 있다.

### 프록시 VS 게이트웨이
- 프록시는 같은 프로토콜을 사용하는 둘 이상의 애플리케이션을 연결함
- 게이트웨이는 서로 다른 프로토콜을 사용하는 둘 이상을 연결함 (프로토콜 변환기)

### 프록시 URI와 서버 URI
- 서버로 요청 ex) GET /index.hmlt HTTP/1.0
- 프록시로 요청 ex) GET http://simjunbo.com/index.html HTTP/1.0
- 프록시는 목적지 서버와 커넥션을 맺어야 하기 때문에, 그 서버의 이름을 알 필요가 있다.

### Via 헤더
- Via 헤더 필드는 메시지가 지나는 각 중간 노드 프록시나 게이트웨이의 정보를 나열한다.
- ex) Via : 1.1 proxy-62.irenes-isp.net, 1.0 cache.joes-hardware.com

## 캐시
### 캐시
- HTTP는 캐시를 효율적으로 동작하게 하고 캐시된 콘텐츠를 최신 버전으로 유지하면서 동시에 프라이버시도 보호하기 위한 많은 기능을 정의한다.
- 캐시는 불필요한 데이터 전송을 줄여서, 네트워크 요금으로 인한 비용을 줄여준다.
- 캐시는 네트워크 병목을 줄여준다. 대역폭을 늘리지 않고도 페이지를 빨리 불러온다.
- 서버에 대한 부하를 줄일 수 있으며 더 빨리 응답할 수 있게 된다.
- 캐시는 거리로 인한 지연을 줄여준다.

### 문서 만료
- HTTP는 Cache-Control과 Expires라는 특별한 헤더들을 이용해서 원 서버가 유효기간을 붙일 수 있게 해준다.

## 게이트웨이
### 게이트웨이
- 게이트웨이는 주로 HTTP 트래픽을 다른 프로토콜로 변환하기 위해 사용된다. ex) HTTP <-게이트웨이-> FTP

## HTTP/2.0
### 등장 배경
- HTTP/1.1 메시지 포맷은 구현의 단순성과 접근성에 주안점을 두고 최적화되다보니 성능은 어느 정도 희생시키지 않을 수 없었다.
- 구글은 웹을 더 빠르게 하겠다는 목표 아래 SPDY(스피디 2009) 프로토콜을 내놓았다.
- SPDY는 헤더를 압축하여 대역폭을 절약했고 하나의 TCP 커넥션에 여러 요청을 동시에 보내 회전 지연(응답을 받아야지 다음 요청을 보냄)을 줄였다.
- 클라이언트가 요청하지 않아도 능동적으로 리소스를 푸시하는 기능도 갖추고 있다.
- 2012년 10월 3일, HTTP 작업 그룹은 SPDY 기반으로 HTTP/2.0 프로토콜 설계를 결정하였다.

### HTTP/1.1과의 차이점
- HTTP/2.0에서 모든 메시지는 프레임에 담겨 전송된다.
- HTTP/1.1에서는 한 TCP 커넥션을 통해 요청을 보낼 때, 응답이 도착하고 나서야 같은 TCP 커넥션으로 다시 요청을 보냈다. 따라서 TCP 커넥션을 여러개 만들어 동시게 요청을 보내는 방법을 사용한다.
- HTTP/2.0에서는 하나의 커넥션에 여러 개의 스트림이 동시에 열릴 수 있다.
- HTTP/1.1에서 헤더는 아무런 압축 없이 그대로 전송된다. HTTP/2.0에서는 메시지의 헤더를 압축하여 전송한다.
- HTTP/2.0은 서버가 하나의 요청에 대해 응답으로 여러 개의 리소스를 보낼 수 있도록 해준다. ex) HTML일 경우 링크하고 있는 image, CSS, Javascript


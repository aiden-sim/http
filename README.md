
### URI (Uniform Resource Identifier)
- 서버 리소스 이름은 통합 자원 식별자, 혹은 URI로 불린다.
- URI에는 두 가지가 있는데, URL과 URN이다. (URI = URL + URN)

### URL (Uniform Resource Locator)
- URL은 특정 서버의 한 리소스에 대한 구체적인 위치를 서술한다. (절대경로)
- 대부분 URL은 세 부분으로 이루어졌다.
	- 스킴 - ex) http://
  - 인터넷 - 주소 ex) www.simjunbo.com
  - 리소스 - ex) /user/simjunbo.gif
  
### URI와 URL의 차이
- 고유의 식별자가 있으면 URI이다.
  - http://simjunbo.com/good.html (URI 이면서 URL)
  - http://simjunbo.com/user/132 (URI)
  
### URN (Unofirm Resource Name)
- 리소스의 위치에 영향 받지 않는 유일무이한 이름


### 메시지
- 웹 클라이언트에서 웹 서버로 보낸 HTTP 메시지를 요청 메시지라고 부른다.
- 서버에서 클라이언트로 가는 메시지는 응답 메시지라고 부른다.
- HTTP 메시지는 세 부분으로 이루어진다.
  - 시작줄 : 요청이라면 무엇을 해야 하는지 응답이라면 무슨 일이 일어났는지
  - 헤더 : key : value 형태로 되어 있고 빈 줄로 끝난다.
  - 본문 : 본문은 임의의 이진 데이터를 포함할 수 있다. 물론 텍스트도 가능
  
### TCP
- TCP는 다음을 제공한다. (UDP 반대)
  - 오류 없는 데이터 전송
  - 순서에 맞는 전달
  - 조각나지 않는 데이터 스트림

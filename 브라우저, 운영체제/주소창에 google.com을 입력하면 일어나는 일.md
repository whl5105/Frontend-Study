### 주소창에 google.com을 입력하면 일어나는 일

1. 사용자가 웹 브라우저를 통해 google.com 을 입력

2. 웹브라우저는 캐싱된 DNS 기록들을 통해 해당 도메인주소와 대응하는 IP주소를 확인

   이 단계에서 캐싱된 기록에 없을 경우, 다음단계로 넘어간다.

   1. 웹브라우저가 HTTP를 사용하여 DNS에게 입력된 도메인 주소를 요청

   2. DNS가 웹브라우저에게 찾는 사이트의 IP주소를 응답

3. 브라우저는 HTTP 프로토콜을 사용하여 요청 메시지를 생성하고 HTTP 요청 메시지는 TCP/IP 프로토콜을 사용하여 서버로 전송

4. 웹브라우저가 웹서버에게 IP주소를 이용하여 html문서를 요청 하며 서버는 response 메시지를 생성하여 다시 브라우저에게 데이터를 전송

5. 브라우저는 response를 받아 파싱하여 화면에 렌더과정을 통해 화면에 웹페이지 내용물 출력

<br/>
<hr/>
<br/>

**DNS**
![8340](https://user-images.githubusercontent.com/73993670/235627267-c6c71d1d-77f0-4cf8-8734-a0302de8eeef.jpeg)

도메인 이름 시스템(DNS)은 사람이 읽을 수 있는 도메인 이름(예: www.amazon.com )을 머신이 읽을 수 있는 IP 주소(예: 192.0.2.44)로 변환합니다. 모든 통신에는 주소가 필요합니다. 출발지와 도착지의 주소를 알아야 통신을 할 수 있습니다. 우리는 이 주소를 IP라고 부릅니다. IP 주소로 변환하는 과정에 개입하는 것이 DNS 입니다.

**URL**

URL(Uniform Resource Locator)은 통합 자원 지시자로 인터넷의 리소스를 가리키는 표준 명칭으로 서버의 자원을 요청할 때 사용됩니다. URL을 통해 인터넷 상의 모든 리소스를 요청할 수 있으며, HTTP, FTP 등의 자원 요청도 가능합니다.

**HTTP**

HTTP(HyperText Transfer Protocol)은 TCP 기반의 클라이언트와 서버 사이에 이루어지는 요청/응답 프로토콜입니다. HTTP는 Text Protocol로 사람이 쉽게 읽고 쓸 수 있습니다. 프로토콜 설계상 클라이언트가 요청을 보내면 반드시 응답을 받아야 합니다. 응답을 받아야 다음 request를 보낼 수 있습니다.

**프로토콜**

프로토콜은 통신하기 위한 약속들을 기술적으로 잘 정의해 둔 것입니다. 데이터를 송수신하는 순서와 내용을 결정합니다. HTTP, TCP/IP, UDP 모두 프로토콜입니다.

<br/>
<hr/>
<br/>

참고 <br/>

https://github.com/Esoolgnah/Frontend-Interview-Questions/blob/main/Notes/important-5/what-happens-when-type-google.md#gear-%ED%94%84%EB%A1%9C%ED%86%A0%EC%BD%9C

https://velog.io/@eassy/www.google.com%EC%9D%84-%EC%A3%BC%EC%86%8C%EC%B0%BD%EC%97%90%EC%84%9C-%EC%9E%85%EB%A0%A5%ED%95%98%EB%A9%B4-%EC%9D%BC%EC%96%B4%EB%82%98%EB%8A%94-%EC%9D%BC

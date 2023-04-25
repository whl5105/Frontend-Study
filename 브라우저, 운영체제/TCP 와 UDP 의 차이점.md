# TCP 와 UDP 의 차이점

## [OSI 모델](https://www.cloudflare.com/ko-kr/learning/ddos/glossary/open-systems-interconnection-model-osi/)
개방형 시스템 상호 연결(OSI) 모델은 표준 프로토콜을 사용하여 다양한 통신 시스템이 통신할 수 있도록 국제표준화기구에서 만든 개념 모델입니다. 쉽게 표현하자면 OSI는 상이한 컴퓨터 시스템이 서로 통신할 수 있는 표준을 제공합니다.

![image](https://user-images.githubusercontent.com/90454621/232481645-6f98f5c1-b7a4-4635-8fc4-3dd7a4dfc38a.png)

<br/>

## TCP(Transmission Control Protocol)

TCP는 클라이언트와 서버가 연결된 상태에서 데이터를 주고받는 연결 지향적 프로토콜입니다.

**TCP는 연속성보다 신뢰성있는 전송이 중요할 때에 사용**하는 프로토콜입니다.

`ex) 파일 전송`

### TCP의 특징
1. 연결형 서비스로 가상 회선 방식을 제공
    - 3-way handshaking과정을 통해 연결을 설정    
    ![image](https://user-images.githubusercontent.com/90454621/232653518-608eb513-78cc-4f67-8b03-a0bfc06c2ec4.png)
    ```
    #1. Client -> Server : 연결 해줘
    #2. Server -> Client : 연결 됐음
    #3. Client -> Server : ㅇㅇ ㄳ
    ```
    - 4-way handshaking과정을 통해 연결을 해제
    ![image](https://user-images.githubusercontent.com/90454621/232653546-253d8544-e203-4567-abac-5d7ba65a5c24.png)
     ```
    #1. Client -> Server : 연결 끊어줘
    #2. Server -> Client : 연결 끊는중
    #3. Server -> Client : 연결 끊었어
    #4. Client -> Server : ㅇㅇ ㄳ
    ```
2. 흐름 제어 
    - 데이터 처리 속도를 조절하여 수신자의 버퍼 오버플로우를 방지
3. 혼잡 제어
    - 네트워크 내의 패킷 수가 과도하게 증가하지 않도록 방지
4. 높은 신뢰성을 보장
    - 신뢰성이 높은 전송을 하기 때문에 UDP보다 속도가 느림 
5. 전이중(Full-Duplex), 점대점(Point to Point) 방식
    - 전이중(Full-Duplex) : 전송이 양방향으로 동시에 일어남
    - 점대점(Point to Point) : 각 연결이 정확히 2개의 종단점을 가짐

<br/>

## UDP(User Datagram Protocol)
UDP는 비연결형 프로토콜입니다.

※ 연결을 위해 할당되는 논리적인 경로가 없고, 각각의 패킷은 다른 경로로 전송되며, 독립적인 관계를 지닙니다.

**UDP는 신뢰성보다는 연속성이 중요할 때에 사용**하는 프로토콜입니다.

`ex) 영상 스트리밍`

### UDP의 특징
1. 비연결형 서비스로 데이터그램 방식을 제공함
    - 데이터의 전송 순서가 바뀔 수 있음
2. 데이터 수신 여부를 확인하지 않음
    - TCP의 3-way handshaking과 같은 과정 X
3. 신뢰성이 낮다.
    - 흐름 제어(flow control)가 없어서 제대로 전송되었는지, 오류가 없는지 확인할 수 없음
4. TCP보다 속도가 빠름
5. 1:1 & 1:N & N:N 통신이 가능

<br/>

## TCP와 UDP의 비교
![image](https://user-images.githubusercontent.com/90454621/232645136-4686f199-1503-4b6f-aaf4-d2e65d82bf89.png)
![TCPvsUDP](https://user-images.githubusercontent.com/90454621/232657365-038ba860-7990-4fd6-b340-92b4b7bb9811.png)

## 요약
TCP는 연속성보다 신뢰성 있는 전송이 중요할 때 사용되는 프로토콜입니다.

UDP는 TCP보다 빠르고 네트워크 부하가 적다는 장점이 있지만, 신뢰성 있는 데이터 전송을 보장하지는 않습니다.

그렇기 때문에 신뢰성보다는 연속성이 중요한 실시간 스트리밍과 같은 서비스에 자주 사용됩니다.

### 참고
https://dev-coco.tistory.com/144#

https://mangkyu.tistory.com/15

https://www.youtube.com/watch?v=ikDVGYp5dhg
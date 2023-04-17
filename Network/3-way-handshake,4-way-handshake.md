**3-way-handshake**

TCP/IP 프로토콜을 이용해서 통신을 하는 응용프로그램이 데이터를 전송하기 전에 먼저 정확한 전송을 보장하기 위해 상대방 컴퓨터와 사전에 세션을 수립하는 과정 (송수신자 사이에 연결을 확인하는 과정)

**4-way-handshake**

세션을 종료하기 위해 수행되는 절차
3way handshake가 연결확립을 위해 진행했다면 4way handshake는 세션을 종료하기 위해 수행되는 절차

<br />
<hr/>

### 3-way-handshake

[State 정보]<br />
CLOSED: 포트가 닫힌 상태 <br />
LISTEN: 포트가 열린 상태로 연결 요청 대기 중 <br />
SYN_RECV: SYNC 요청을 받고 상대방의 응답을 기다리는 중 <br />
ESTABLISHED: 포트 연결 상태<br />
TIME-WAIT: Server로부터 FIN을 수신하더라도 일정시간(default: 240초)동안 세션을 남겨놓고 잉여 패킷을 기다리는 과정 <br />

**SYN(Synchronize Sequence Number)**
1. 활성 오픈이되면 클라이언트가 서버에 SYN을 전송하여 수행합니다.<br />

**SYN-ACK**
1. Server는 Listen상태에서 SYN가 들어온 것을 확인합니다. <br />
2. SYN 수신이 확인되면 SYN_RECV상태로 바뀌어 SYN-ACK로 응답합니다. <br />
3. ACK 번호는 수신된 시퀀스보다 하나 더 큰 A+1로 설정되며, 서버가 패킷에 대해 선택한 시퀀스 번호는 또 다른 임의의 숫자인 B입니다. <br />
4. 그 후 Server는 다시 ACK 플래그를 받기 위해 대기상태로 변경됩니다. <br />

**ACK(Acknowledgement)**
1. SYN + ACK 상태를 확인한 Client는 서버에게 ACK를 보냅니다.<br />
    시퀀스 번호는 수신된 승인 값 즉 A+1로 설정되고 ,승인 번호는 수신된 시퀀스 번호 즉 B+1보다 하나 큰 값으로 설정됩니다.<br />
2. 연결 성립(Established)이 됩니다.<br />

<br />

1단계와 2단계는 한 방향에 대한 시퀀스 번호를 설정하고 승인합니다.<br />
2단계와 3단계는 다른 방향에 대한 시퀀스 번호를 설정하고 승인합니다.<br />
이 단계를 완료하면 클라이언트와 서버 모두 승인을 받고 전이중 통신이 설정됩니다<br />

<hr/>

### 4-way-handshake

**FIN**
1. Client가 연결을 종료하겠다는 FIN플래그를 전송합니다.
2. FIN-WAIT-1 상태로 변경됩니다.

**ACK(Acknowledgement)**
1. FIN 플래그를 받은 Server는 확인메세지인 ACK를 Client에게 보내줍니다.
2. CLOSE-WAIT상태로 변경됩니다.
3. Client도 Server에서 FIN을 받기위해 FIN-WAIT-2 상태로 변경됩니다.

**FIN**
1. Server는 Close준비가 다 된 후 Client에게 FIN 플래그를 전송합니다.

**ACK(Acknowledgement)**
1. Client는 해지 준비가 되었다는 정상응답인 ACK를 Server에게 보냅니다.
2. Client는 TIME-WAIT 상태로 변경됩니다.
    TIME-WAIT 시간동안(일부 공통 값은 30초, 1분 ~ 2분) 로컬 포트는 새 연결을 할 수 없습니다.
3. TIME-WAIT 상태는 의도치않은 에러로 인해 연결이 데드락으로 빠지는 것을 방지 하며, 만약 에러로 인해 종료가 지연되다가 타임이 초과되면 CLOSED 상태로 변경됩니다.

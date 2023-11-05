# TCP 의 연결 및 해제 과정 (3,4-way hands shaking)

## Transport Layer
Transport Layer에는 양 끝단(End to end)의 사용자들이 신뢰성있는 데이터를 주고 받을 수 있도록 해 주어, 상위 계층들이 데이터 전달의 유효성이나 효율성을 생각하지 않도록 해준다.  
  
전송 프로토콜로 잘 알려진 것이 TCP와 UDP이다. 
[![](./img/network_img_4.PNG?width=300px)]()  

#### :pushpin: Transport Layer VS Network Layer
Transport Layer : Application 프로세스들 간의 논리적인 통신을 제공  
Network Layer : host 간의 논리적인 통신을 제공(데이터의 전달 경로를 설정하는 역할)

## TCP (Transmission Control Protocol)
인터넷상에서 데이터를 메세지의 형태로 보내기 위해 IP와 함께 사용하는 프로토콜

TCP는 애플리케이션에게 `신뢰적`이고 `연결지향성 서비스`를 제공한다. 일반적으로 TCP와 IP는 함께 사용되며 IP는 배달을, TCP는 패킷의 추적 및 관리를 하게 됩니다.

TCP는 연결형 서비스로, 신뢰적인 전송을 보장하기에 `hanshaking`하고 데이터의 `흐름제어`와 `혼잡제어`를 수행합니다. 하지만 이러한 기능으로 인해 TCP의 `속도는 느립니다.`
  
**TCP 특징**
- 3-way handshaking과정을 통해 연결을 설정하고 4-way handshaking을 통해 해제한다.
- 흐름 제어 및 혼잡 제어.
- 높은 신뢰성을 보장한다.
- UDP보다 속도가 느리다.
- 전이중(Full-Duplex), 점대점(Point to Point) 방식.


## UDP (User Datagram Protocol)
데이터를 데이터그램(독립적인 단위를 가지는 패킷) 단위로 처리하는 프로토콜 

UDP는 `비연결형` 프로토콜이다. 즉, 할당되는 논리적인 경로가 없고 **각각의 패킷이 다른 경로로 전송되고 이 각각의 패킷은 독립적인 관계**를 지니게 되는데, 이렇게 데이터를 서로 다른 경로로 독립 처리하는 프로토콜을 UDP 라고 합니다.

UDP는 연결을 설정하고 해제하는 과정이 존재하지 않는다. 서로 다른 경로로 독립적으로 처리함에도 패킷에 순서를 부여하여 재조립하거나 흐름제어 및 혼잡제어를 수행하지 않아 `속도가 빠르며` 네트워크 부하가 적다는 장점이 있지만 데이터 전송의 `신뢰성이 낮다`. 연속성이 중요한 `실시간 서비스(스트리밍)`에 좋다.
  
**UDP 특징**
- 비연결형 서비스로 데이터그램 방식을 제공한다
- 정보를 주고 받을 때 정보를 보내거나 받는다는 신호절차를 거치지 않는다.
- UDP헤더의 CheckSum 필드를 통해 최소한의 오류만 검출한다.
- 신뢰성이 낮다
- TCP보다 속도가 빠르다  
<br>  
  
[![](./img/network_img_5.PNG?width=300px)]()
<br>

### :pushpin: 포트(PORT) 상태 정보
- **CLOSED**: 포트가 닫힌 상태
- **LISTEN**: 포트가 열린 상태로 연결 요청 대기 중
- **SYN_RCV**: SYNC 요청을 받고 상대방의 응답을 기다리는 중
- **ESTABLISHED**: 포트 연결 상태

### :pushpin: 플래그 정보
#### SYN(Synchronize Sequence Number)
> 연결 설정. Sequence Number를 랜덤으로 설정하여 세션을 연결하는 데 사용하며, 초기에 Sequence Number를 전송한다.
#### ACK(Acknowledgement)
> 응답 확인. 패킷을 받았다는 것을 의미한다.  
> Acknowledgement Number 필드가 유효한지를 나타낸다.  
> 양단 프로세스가 쉬지 않고 데이터를 전송한다고 가정하면 최초 연결 설정 과정에서 전송되는 첫 번째 세그먼트를 제외한 모든 세그먼트의 ACK 비트는 1로 지정된다고 생각할 수 있다.
#### FIN(Finish)
> 연결 해제. 세션 연결을 종료시킬 때 사용되며, 더 이상 전송할 데이터가 없음을 의미한다.

## 3-way HandShake

3-Way Handshake : TCP의 접속

### 3-way HandShake의 개념

- TCP 통신을 이용하여 데이터를 전송하기 위해 **네트워크 연결을 설정(Connection Establish) 하는 과정**
- 양쪽 모두 데이터를 전송할 준비가 되었다는 것을 보장하고, 실제로 데이터 전달이 시작하기 전에 한 쪽이 다른 쪽이 준비되었다는 것을 알 수 있도록 한다.
- 즉, TCP/IP 프로토콜을 이용해서 통신을 하는 응용 프로그램이 데이터를 전송하기 전에 먼저 정확한 전송을 보장하기 위해 상대방 컴퓨터와 사전에 ~세션을 수립하는 과정~을 의미한다.


### 3-way HandShake의 과정
[![](./img/network_img_6.PNG?width=300px)]()
  
1. A클라이언트는 B서버에 접속을 요청하는 SYN 패킷을 보낸다. 이때 A클라이언트는 SYN 을 보내고 SYN/ACK 응답을 기다리는SYN_SENT 상태가 되는 것이다.  
2. B서버는 SYN요청을 받고 A클라이언트에게 요청을 수락한다는 ACK 와 SYN flag 가 설정된 패킷을 발송하고 A가 다시 ACK으로 응답하기를 기다린다. 이때 B서버는 SYN_RECEIVED 상태가 된다.  
3. A클라이언트는 B서버에게 ACK을 보내고 이후로부터는 연결이 이루어지고 데이터가 오가게 되는것이다. 이때의 B서버 상태가 ESTABLISHED 이다.  

위와 같은 방식으로 통신하는것이 신뢰성 있는 연결을 맺어 준다는 TCP의 3 Way handshake 방식이다.  
<br>

## 4-way HandShake

4-Way Handshake : TCP의 접속 해제 과정, 여기서는 FIN 플래그를 이용

### Termination의 종류
- Graceful connection release(정상적인 연결 해제)
    > 정상적인 연결 해제에서는 양쪽이 커넥션이 서로 모두 커넥션을 닫을 때까지 연결되어 있다.

- Abrupt connection release(갑작스런 연결 해제)
    > 갑자기 한 TCP 엔티티가 연결을 강제로 닫는 경우  
    > 한 사용자가 두 데이터 전송 방향을 모두 닫는 경우

### 4-way HandShake의 과정
[![](./img/network_img_7.PNG?width=300px)]()  
1. 클라이언트가 연결을 종료하겠다는 FIN플래그를 전송한다.
2. 서버는 일단 확인메시지를 보내고 자신의 통신이 끝날때까지 기다리는데 이 상태가 TIME_WAIT상태다.
3. 서버가 통신이 끝났으면 연결이 종료되었다고 클라이언트에게 FIN플래그를 전송한다.
4. 클라이언트는 확인했다는 메시지를 보낸다.

# :question: 예상 질문

<details>
  <summary><b>TCP의 연결 설정 과정(3단계)과 연결 종료 과정(4단계)이 단계가 차이나는 이유는 무엇인지 설명하시오.</b></summary>
  <div markdown="1">
    Client가 데이터 전송을 마쳤다고 하더라도 Server는 아직 보낼 데이터가 남아있을 수 있기 때문에 일단 FIN에 대한 ACK만 보내고, 
    데이터를 모두 전송한 후에 자신도 FIN 메시지를 보내기 때문이다.
  </div>
</details>
<details>
  <summary><b>만약 Server에서 FIN 플래그를 전송하기 전에 전송한 패킷이 Routing 지연이나 패킷 유실로 인한 재전송 등으로 인해 FIN 패킷보다 늦게 도착하는 상황이 발생하면 어떻게 될까?</b></summary>
  <div markdown="1">
    이러한 현상에 대비하여 Client는 Server로부터 FIN 플래그를 수신하더라도 일정시간(Default: 240sec)동안 세션을 남겨 놓고 잉여 패킷을 기다리는 과정을 거친다. (TIME_WAIT 과정)
  </div>
</details>
<br>
    
# :newspaper: Reference

[handshake](https://mindnet.tistory.com/entry/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-%EC%89%BD%EA%B2%8C-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-22%ED%8E%B8-TCP-3-WayHandshake-4-WayHandshake)
[TCP/UDP](https://velog.io/@averycode/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-TCPUDP%EC%99%80-3-Way-Handshake4-Way-Handshake)



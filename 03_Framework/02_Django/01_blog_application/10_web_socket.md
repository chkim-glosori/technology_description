# Web Socket

## 1. Web Socket 이란?
WebSocket 은 웹 브라우저와 서버 간의 양방향 통신을 가능하게 하는 프로토콜이다. HTTP 를 기반으로 하여 초기 연결을 설정한 후, 지속적인 연결을 유지하면서 실시간으로 데이터를 송수신할 수 있다.

WebSocket 은 클라이언트와 서버 간의 데이터 전송을 효율적으로 처리하며, 특히 실시간 웹 애플리케이션에서 많이 사용된다.

일반적인 Server-Client 구조 & HTTP 프로토콜을 이용한 통신 구조와는 다르게, 클라이언트와 서버가 초기 핸드셰이크 이후 연결을 항상 유지하는 방식이다.

그에 따라, 클라이언트와 서버가 서로 데이터를 주고 받을 수 있고, 연결이 유지되어 있기 때문에 데이터 전송을 위한 오버헤드가 줄어 들며, 데이터 전송 시 HTTP 요청-응답 사이클을 생략하여 빠른 응답이 가능하다.

## 2. 전통적인 서버 - 클라이언트 구조가 통신하는 방식
전통적인 서버-클라이언트 구조에서는 클라이언트가 요청을 보내면 서버가 응답하는 방식으로 작동한다.

- HTTP 프로토콜 사용: 클라이언트는 서버에 HTTP 요청을 보내고, 서버는 요청에 대한 응답을 반환한다.
- 단방향 통신: 클라이언트가 요청을 보낼 때마다 새로운 연결이 생성되고, 서버는 요청에 대한 응답만을 전송한다.
- 상태 비저장: 각 요청은 독립적이며, 서버는 클라이언트의 상태를 기억하지 않는다.

## 3. Web Socket 구조가 통신하는 방식
Web Socket 구조에서는 클라이언트와 서버 간에 지속적인 연결이 유지된다. 초기 연결은 HTTP 를 통해 핸드셰이크로 설정되며, 이후에는 WebSocket 프로토콜을 사용하여 데이터를 송수신한다.

### 통신 과정
1. 핸드셰이크 : 클라이언트가 서버에 WebSocket 연결 요청을 보낸다.
    1. 클라이언트가 WebSocket 연결을 요청하는 HTTP 요청을 서버에 보낸다. 이 요청에는 Upgrade 헤더가 포함되어 있다.
    2. 서버가 요청을 수락하면, 클라이언트에게 101 Switching Protocols 응답을 보내고 WebSocket 프로토콜로 전환한다.
2. 연결 수립 : 위 단계에서 서버 간의 WebSocket 연결이 수립된다.
3. 데이터 전송 : 연결이 유지되는 동안 클라이언트와 서버는 양방향으로 데이터와 자유롭게 송수신할 수 있다.
4. 연결 종료 : 필요에 따라 클라이언트 또는 서버가 연결을 종료할 수 있다.

이 과정은 HTTP 요청-응답 방식으로 이루어지며, TCP 연결이 이미 설정되어 있어야 한다. 따라서, WebSocket 의 핸드셰이크는 TCP 연결 위에서 이루어지는 추가 단계이다.

### TCP 의 Three-Way Handshake
TCP 연결을 수립하기 위한 Three-Way Hanshake 는 다음과 같은 단계로 이루어진다.

1. SYN : 클라이언트가 서버에 연결 요청 (SYN)을 보낸다.
2. SYN-ACK : 서버가 클라이언트의 요청을 수락하고 확인 응답(SYN-ACK)을 보낸다.
3. ACK : 클라이언트가 서버의 응답을 확인하는 ACK 패킷을 보내며, 이로써 TCP 연결이 수립된다.

### 결론
WebSocket 의 핸드셰이크는 TCP 연결이 수립된 후에 추가로 이루어지는 과정이다. 따라서 WebSocket 핸드셰이크는 TCP 의 Three-Way Handshake 와는 별개의 과정이다. WebSocket 은 TCP 연결을 기반으로 하며, 초기 핸드셰이크가 완료된 후에는 양방향 통신을 위해 지속적인 연결을 유지한다.

## 4. 전통적인 서버 - 클라이언트와 구조하여 장단점 분석
| 특징               | 전통적인 서버-클라이언트 구조 | WebSocket 구조               |
|------------------|----------------------------|-----------------------------|
| **통신 방식**      | 단방향 통신                | 양방향 통신                 |
| **연결 유지**      | 요청-응답 방식으로 매번 새로운 연결 생성 | 지속적인 연결 유지         |
| **데이터 전송**    | 요청 시에만 데이터 전송    | 실시간으로 데이터 전송 가능 |
| **오버헤드**       | 높은 오버헤드 (매 요청마다 연결 설정) | 낮은 오버헤드              |
| **상태 관리**      | 상태 비저장                | 상태 유지 가능              |
| **사용 사례**      | 일반적인 웹 페이지 요청    | 실시간 애플리케이션 (채팅, 게임 등) |

### 장점
- WebSocket : 실시간 데이터 전송, 낮은 지연 시간, 효율적인 데이터 처리, 클라이언트와 서버 간의 상태 유지.
- 전통적인 서버-클라이언트 : 구현이 간단하고, HTTP 프로토콜에 익숙한 개발자에게 친숙하다.

### 단점
- WebSocket : 초기 설정이 복잡할 수 있으며, 모든 브라우저나 서버가 지원하지 않을 수 있다.
- 전통적인 서버-클라이언트 : 실시간 기능 부족, 높은 오버헤드로 인한 성능 저하, 상태 비저장으로 인한 불편함.
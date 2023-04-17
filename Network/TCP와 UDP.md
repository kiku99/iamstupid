# Transport Layer

End Point간 신뢰성있는 데이터 전송을 담당하는 계층

+ 신뢰성: 데이터를 순차적, 안정적인 전달
+ 전송: 포트 번호에 해당하는 프로세스에 데이터를 전달

## 전송 계층이 없다면 (전송 계층의 중요성)

+ 데이터의 순차 전송이 원활하지 않다
+ 송수신자 간의 데이터 처리 속도 차이 때문에 흐름 문제가 발생한다
+ 네트워크의 데이터 처리 속도 때문에 혼잡 문제가 발생한다


# TCP (Transmission Control protocol)

+ 신뢰성있는 데이터 통신을 가능하게 해주는 프로토콜
+ 특징: Connection 연결 (3 way-handshake) - 양방향 통신
+ 데이터의 순차 전송을 보장
+ Flow Control (흐름 제어)
+ Congestion Control (혼잡 제어)
+ Error Detection (오류 감지)

## 세그먼트 (Segment) - TCP 프로토콜의 PDU

+ TCP Header를 Data에 추가해서 만든 단위
+ TCP Header안에서 9bit의 flag field가 중요함
    + SYN: TCP가 Connection을 연결할 때 사용하는 flag bit
    + FIN: Connection을 끊을 떄 사용하는 flag bit
    + ACK: Data를 받는 사람이 다시 전송할 때 제어의 목적으로 사용하는 flag bit

## TCP의 3-way handshake (Connection 연결)

1. Client는 SYN비트를 1로 설정해 패킷 송신 (클라이언트가 서버에 연결 요청)
2. Server는 SYN, ACK비트를 1로 설정해 패킷 송신 (서버가 데이터를 받고 통로를 같이 연결하고 싶다고 요청)
3. Client는 ACK비트를 1로 설정해 패킷 송신 (통로를 연결하고 ok사인을 보냄)

## TCP의 문제점

+ 전송의 신뢰성은 보장하지만 매번 connection을 연결해서 시간손실 발생
+ 패킷으 조금만 손실해도 재전송
+ 서비스에 따라 불합리함


# UDP (User Datagram protocol)

+ TCP보다 신뢰성이 떨어지지만 전송 속도가 일반적으로 빠른 프로토콜
+ Connectionless
+ Error Detection
+ 비교적 데이터의 신뢰성이 중요하지 않을 때 사용 (영상 스트리밍)

## UDP의 데이터 전송 방식

+ 클라이언트가 패킷 송신 (단방향)


# 중요한 점

+ TCP, UDP의 특성을 파악하고 상황에 따라 적절한 프로토콜을 사용할 수 있다
+ TCP, UDP의 헤더에 대해 파악하고 성능 개선에 이용할 수 있다


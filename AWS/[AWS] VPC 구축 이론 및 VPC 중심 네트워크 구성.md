# AWS VPC 구축 이론 및 VPC 중심 네트워크 구성

## AWS VPC

### Virtual Private Network(VPN)

- VPN은 인터넷을 통해 디바이스 간에 네트워크 연결을 생성한다.
- VPN은 퍼블릭 네트워크를 통해 데이터를 안전하게 익명으로 전송하는 데 사용된다. 
- 또한 사용자 IP주소를 마스킹하고 데이터를 암호화하여 수신 권한이 없는 사람이 읽을 수 없도록 한다. 

![image](https://user-images.githubusercontent.com/66311161/177533875-7abbf68a-5707-46f5-a781-fa1504674721.png)

### Virtual Private Cloud(VPC)

- Amazon Virtual Private Cloud(Amazon VPC)는 사용자가 정의한 가상 네트워크이다.
- 사용자가 구성요소들을 이용하여 원하는 형태로 네트워크망을 구축할 수 있다.

![image](https://user-images.githubusercontent.com/66311161/177534508-b9501695-c10c-42a0-93a9-f2dc9586723d.png)

### VPC 구성 요소

Subnet – VPC를 특정 범위로 나눈 범위
RouteTable – 네트워크 트래픽을 전달한 위치가 명시된 규칙 집합 테이블
Internet GW – VPC의 리소스에서의 인터넷 통신을 활성화하기 위한 게이트 웨이
NAT GW – 네트워크 주소 변환을 통해 private subnet에서 인터넷 통신을 연결하는 게이트웨이
VPC endpoint – NAT, IGW 등을 통하지 않고 AWS의 서비스를 비공개로 연결 가능하게 하는 서비스

![image](https://user-images.githubusercontent.com/66311161/177536777-0bed66b9-cbc8-418a-8e3d-bdbbe07a4bac.png)

### CIDR(Classless Inter-Domain Routing)

- 클래스 없이 유연하게 네트워크 영역을 나누어 IP주소를 할당하는 방식

## VPC 중심 네트워크 구성

## VPC 대역 정하기

- IPv4의 경우 /16(65,536) ~ /28(16개) 넷마스크 허용
- RFC 1918에 정의된 사설 IP대역 사용 권장
  - 10.0.0.0/8: 10.0.0.0 ~ 10.255.255.255
  - 172.16.0.0/12: 172.16.0.0 ~ 172.31.255.255
  - 192.168.0.0/16: 192.168.0.0 ~ 192.168.255.255
- VPC CIDR 변경 불가, 대역 추가는 가능
  - (선택사항) IPv6sms VPC 대역은 /56, 각 서브넷은 /64 고정
- 서브넷마다 예약된 IP 고려 필요 (예: 10.1.0.0/24)

## VPC Subneting

![image](https://user-images.githubusercontent.com/66311161/177537907-709b76b0-b89c-4437-b68a-2808a20603aa.png)









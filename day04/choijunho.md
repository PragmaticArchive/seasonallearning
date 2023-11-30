# Server Management

## 서버관리와 리눅스

> OS

- Windows
- Linux

> Why Linux?

1. Free and Open Source
   - 무료 오픈소스
2. Stability
   - Window가 Linux보다 바이러스에 취약하다.
   - Open source로 인해 많은 Linux 사용자가 존재하고 이들이 빠른 시간 내에 취약점을 해결한다.
3. Secure and Flexibility
   - 사용자가 원하는 목적에 맞게 시스템을 자유롭게 변경할 수 있다.

> 리눅스의 종류

- 슬랙웨어 : 안정성이 좋음
- 데비안 : 사용자가 많음 (ex Unbuntu)
- 레드햇 : 회사가 직접 관리 (ex Pedora, CentOS)

## 서버관리와 네트워크

> NAT(Network Address Translation / 네트워크 주소 변환)

- 내부 네트워크에서 외부 네트워크로 단방향 연결, host 내부 네트워크와 통신 불가
- 호스트와 내부 게스트간 통신을 하려면 포트포워딩(이정표) 필요

인터넷 ↔ 라우터(Router 공유기) ↔ Host ↔ Guest(가상머신)

- Host(192.168.0.1)
- Guest01(10.0.2.15:80)
- Guest02(10.0.2.15:80)

> Adapter에 Bridge

- 외부 라우터에서 IP주소 직접 받아옴
- Host(192.168.0.1)
- Guest01(192.168.0.2)
- Guest02(192.168.0.3)

> NAT NETWORK

- NAT 방식과 비슷하지만 내부 네트워크의 게스트간 통신 가능
- DHCP에 의해 IP address를 자동으로 할당 받음
- NAT과 마찬가지로 포트포워딩 필요
- Host(192.168.0.1)
- Guest01(192.168.0.1:80 → 10.0.2.15:80)
- Guest02(192.168.0.1:81 → 10.0.2.16:80)

※ DHCP : TCP/IP 통신을 실행하기 위해 필요한 IP를 자동적으로 할당, 관리하기 위한 통신 규약(프로토콜)

#### continue

# Computer Science
- 운영체제, 컴파일러
- 네트워크
- 자료구조 - 알고리즘
- 컴퓨터구조
- 데이터베이스
- 소프트웨어공학

# 운영체제
## File Management

### 파일은 어떻게 실행되는 것일까?
- 운영체제에서 PDF, JPG 등을 인식해서 적절한 프로그램을 함께 실행시켜준다.

### 파일 확장자 (File Extention)
- `.pdf`, `.exe`, `.jpg`와 같이 파일 이름 뒤에 `.`으로 구분하여 사용하는 것을 말합니다.
- 운영체제는 파일 확장자를 인식해서 파일의 종류를 파악하고, 아이콘과 프로그램을 매칭시켜준다.
	- 모든 운영체제가 확장자를 통해 분류하는 것은 아님!
 
### 파일 시그니처 (File Signature)
- File magic number나 File Cheksum을 참조하여 파일의 내용을 검증하거나 식별하는데 사용하는 데이터

### 파일 매직 넘버 (File Magic Number)
- 여러 운영체제에서 공통적으로 사용되며, 간단하고 효과적인 파일 형식을 구별하는 값.

| Extension | Offset | Hex value |
|---|---|---|
|.zip .pptx<br>.docx .apk<br>.jar ... | 0 | `50 4B 03 04`|
| .ext .dll<br>.sys ... | 0 | `4D 5A` |
| .png | 0 | `89 50 4E 47 0D 0A 1A 0A` |

### 파일 체크섬 (File Checksum)
- 에러를 탐지하기 위한 작은 크기의 데이터 블록
검증 방법
- 검증 비트를 만든다.
	- 패리티 비트
		- 7비트 데이터 중 1인 bit의 개수를 확인하여 홀수 또는 짝수로 만들어 에러를 확인
	- CRC
		- CRC는 방식이 많다.
		- CRC-8 : `x^8 + x^2 + x^1 + 1

### 헤더 (Header)
파일 -> 확장자 -> 연결프로그램 -> 파일 시그니처 -> 매직 넘버 -> 체크섬 (패리티 비트(CRC-1) or CRC)

### HDD (Hard Disk Drive) 구조
- Cylinder : 여러 개의 Platter로 구성
- Platter : 여러 개의 Track으로 구성
- Track : 여러 개의 Sector로 구성
- Sector : 데이터를 저장하는 공간
- Arm : Cylinder의 위치 이동
- Head : Sector의 데이터를 읽고 씀

<img width="386" alt="Pasted image 20231128162407" src="https://github.com/MadCom96/seasonallearning/assets/70102600/443c3463-bfc1-4367-b1d2-6ca9513a7626">


i. Sector (Block)
파일의 크기가 1KB이더라도 4KB공간을 모두 사용하며, 남은 공간은 의미 없는 데이터로 채운다.
ii. Partition
하나의 HDD를 논리적으로 나누어 사용하는 방법을 말한다.
C드라이브, D드라이브로 나누어 사용하는 경우, C드라이브는 0~99번 실린더를 D드라이브는 100~199 실린더를 사용하게 된다.

**딜레이**
- Seek Time
	- Head가 원하는 트랙까지 찾아가는 시간. Head의 위치에 따라 Track을 찾아가는 시간이 다르기 때문에 평균 시간을 이용한다.
- Rotational Delay(Latency)
	- 현재 Sector에서 읽고자 하는 Sector까지 회전하여 Head 밑까지 오는 시간
- Transfer Time
	- 디스크 표면에서 데이터를 읽어 메모리로 이동하는 시간. 메모리로 이동하는 시간은 짧기 때문에 디스크에서 읽는 시간이 전부이다.

### Disk Scheduling
- 필요한 데이터를 찾기 위해서 Track을 어떤 순서대로 찾아가는지에 대한 방법
- First-in First-Out
- Shortest Service Time First (SSTF) : 현재 Head의 위치와 가장 가까운 Track을 먼저 탐색하는 방법
- SCAN : Head가 들어가면서 순차적으로 Track을 탐색하고, 나오면서 순차적으로 Track을 탐색하는 방법
- Cyclic-SCAN : Head가 들어가면서 순차적으로 Track을 탐색하고, 나오면서는 탐색하지 않는다.
- FSCAN : 두 개의 Queue를 사용하며 SCAN과 동일한 방식으로 탐색하는 방법. 추가 요청이 발생하는 경우 다음 Queue에서 대기.
- 4-Step-SCAN : Queue에 도착한 Track들을 4개씩 나누어 SCAN 방식으로 탐색하는 방법.

### File Allocation
Disk에 파일을 어떻게 Write할 것인지. 파일을 Read할 때 어떻게 찾아갈 것인지.
`Contiguous Allocation`, `ChainedAllocation`, `Indexed Allocation` 방법 들이 있다.

##### Contiguous Allocation
디스크의 연속된 빈 블록에 저장하는 방식으로, 파일 생성 시 파일의 크기를 미리 알고 있어야 한다.
연속된 빈 공간에 파일을 기록하는 방식인 만큼. 비어있는 공간이 발생한다.
- 빈 공간을 제거하기 위해 Compaction을 진행한다. 빈공간 발생마다 매번 Compaction을 진행하는 것은 매우 비효율적이다.
##### Chained Allocation
각 블록을 연결하는 방식으로, 연속된 빈 블록이 필요없다.
FAT16, FAT32에서 이 방식을 응용하여 사용한다.
- FAT : 파일의 데이터 블록을 찾아가는 정보를 저장하고 있는 테이블

<img width="551" alt="Pasted image 20231128165738" src="https://github.com/MadCom96/seasonallearning/assets/70102600/bb349f6b-7a27-46d3-8c06-7c4518e285a7">



##### Indexed Allocation
Index를 사용하여 파일을 저장하는 방식으로, NTFS에서 이 방식을 응용하여 사용한다.
- Index Block 하나에 1024개의 블록 번호를 가질 수 있다.

<img width="313" alt="Pasted image 20231128165838" src="https://github.com/MadCom96/seasonallearning/assets/70102600/d29f7e5e-ec78-45c7-9198-73384ace6ecd">




## Memory Management
### Partitioning
물리적 영역을 나누는 방법으로 Fixed와 Dynamic방식이 있다.

### Fixed Partitioning
고정된 크기로 메모리 공간을 나누어 사용하는 방식으로, Equal-Size와 Unequal-Size 방식이 있다.

### Dynamic Partitioning
고정된 크기로 메모리 공간을 필요한 만큼 동적으로 나누어 사용하는 방식.

<img width="940" alt="Pasted image 20231128170317" src="https://github.com/MadCom96/seasonallearning/assets/70102600/c0937c1a-76e1-4388-ad78-687b658acc45">

##### First-Fit
처음부터 확인해서 할당할 수 있는 공간에 할당하는 방식
##### Best-Fit
최대한 딱 맞는 공간에 할당하는 방식
##### Next-Fit
마지막 할당 이후를 확인해서 할당할 수 있는 공간에 할당하는 방식

### Frames & Pages
Stack : 함수, 지역변수/ 낮 -> 높
Heap : 전역변수, 동적할당/ 높 -> 낮
##### Page Number 
프로그램을 일정 크기로 나눈 공간
명령어, 변수들이 포함되어 있다.
##### Frame Number
메모리를 일정 크기로 나눈 공간

- 우리가 사용하는 메모리 주소는 모두 논리 주소(가짜 주소)이며, 물리 주소(실제 주소)로  변환하기 위해 Memory Management Unit(MMU)를 사용한다.
- 프로그램은 메모리에 올라가면 프로세스라 표현하고, 프로그램을 실행 시키기 위해서는 모든 내용이 메모리에 올라가 있어야 한다.
- 메모리는 1GB이고, 프로그램이 4GB라면 어떻게 되나요?
	- 가상 메모리 사용!

### Virtual Memory
메모리에는 필요한 내용만 올려두고 나머지 내용은 HDD에 저장해 두어 사용하는데, HDD는 실제 Memory가 아니므로 이를 Virtual Memory라 말한다.
메모리에 다음 명령어가 존재하지 않으면 Page Fault가 발생하고, HDD에서 다음 명령어 Page를 가져온다.
(Swap out, Swap in)
- 일부 내용만 메모리에 사용하는 이유는 무엇일까?
	- 프로세스는 일부만 메모리에 올려두고 나머지는 가상 메모리를 사용하는데, 프로세스가 일정 시간 동안 몇 개의 Page만을 참조하기 때문이며, 이를 Locality(지역성) 이라 말한다.
- 일부만 필요하다면, 프로그램을 엄청 많이 실행해도 상관 없겠네요?
	- 프로세스의 수가 증가하면 하나의 프로세스에 할당되는 Frame 수는 줄어들게 되고, 메모리에 올라간 명령어가 적어지므로 Page Fault 수가 증가하며, CPU는 Page Fault를 처리하느라 이용률이 떨어지게 된다. (Thrashing)

### Replacement Policy
Page Fault가 발생하는 경우 비어있는 공간이 없다면, 어떤 Page를 Swap Out할 지를 선택하는 방법.

##### Optimal Policy
향후 가장 오랫동안 참조되지 않을 Page를 선택하는 방법.
성능은 가장 좋지만, 구현이 불가능하다.

##### Least Recently Used (LRU)
최근에 가장 오랫동안 참조되지 않은 Page를 선택하는 방법.
참조했던 Page에 시간을 저장해야하기 때문에 Overhead가 크다.

##### First-In, First-Out (FIFO)
메모리에 먼저 올라왔던 Page 순서대로 선택하는 방법.
구현은 가장 간단하지만, 성능은 가장 좋지않다.

### Clock Policy
page가 참조되는 경우 use bit의 값을 1로 설정하고, 참조되지 않은 Page를  찾아 교체하는 방법.
최초 메모리에 올라가는 경우 use bit 값을 1로 설정한다.

교체 대상 Page를 찾기 위해서 use bit가 0인 Page를 찾고, use bit가 1이었던 Page를 0으로 변경.

<img width="740" alt="Pasted image 20231128175158" src="https://github.com/MadCom96/seasonallearning/assets/70102600/c7ab4f73-a3d1-4fe0-b0fc-bace8dc245f4">



## Scheduling
프로세스를 어떻게 관리하는지에 대한 방법.
##### Nonpreemptive (비선점형)
Interrupt로 인한 프로세스 스위칭이 발생하지 않고, 원래 실행되는 프로세스가 온전히 끝나야만 다음 프로세스가 실행되는 방법
##### Preemptive (선점형)
Interrupt로 인한 프로세스 스위칭이 발생하고, 우선 순위가 더 높은 프로세스가 CPU를 선점하는 방법

### First-Come-First-Served (FCFS) - 비선점
먼저 Ready Queue에 들어온 프로세스 순서대로 진행하는 방법. (FIFO)
짧은 작업의 프로세스는 긴 작업의 프로세스 때문에 오랫동안 기다려야 하는 문제점이 발생

### Shortest Process Next (SPN) - 비선점
서비스 시간이 짧은 프로세스가 먼저 실행하는 방법 (가로채지는 않는다.)
서비스가 다 끝난 뒤에 결정되는 것이므로 선점형이 아니다.
서비스 시간이 긴 프로세스는 실행되지 않을 수 있는 문제가 발생한다. (Starvation)

### Highest Response Ratio Next (HRRN) - 비선점
Ready Queue에서 기다린 시간과 서비스 해야하는 시간을 계산하여 다음 프로세스를 결정하는 방법.

### Round-Robin - Preemptive (At Time Slice, Time Quantum)
번갈아가면서 시간으로 잘라 프로세스를 실행한다.

### Shortest Remaining Time (SRT) - 선점
남아있는 시간이 짧은 프로세스를 실행시키는 방법.
SPN의 선점형 방식이다.

### Shortest Process Next (SPN) - 비선점
서비스 시간이 짧은 프로세스가 먼저 실행하는 방법.
서비스가 다 끝난 뒤에 결정되는 것이므로 선점형이 아니다.
서비스 시간이 긴 프로세스는 실행되지 않을 수 있는 문제가 발생한다. (Starvation)

---
### Process Switch

<img width="1008" alt="Pasted image 20231128181148" src="https://github.com/MadCom96/seasonallearning/assets/70102600/a2b4a317-8bab-41b8-8b6a-cead71b750fb">


### Process Control Block (PCB)
운영체제 내에서 관리되는 프로세스 구조체

<img width="273" alt="Pasted image 20231128181302" src="https://github.com/MadCom96/seasonallearning/assets/70102600/7200d517-830a-4a6c-9e7b-c746e0340fe0">

- Process : 자원의 소유자 역할, CPU를 할당하는 대상이 아니다. 실행 코드, 전역 변수, 힙과 같은 자원의 소유주 역할. 하나의 프로세스는 기본적으로 하나의 Main Thread를 갖는다.
- Thread : CPU에 할당되는 대상으로 하나의 Process는 여러 개의 Thread를 가질 수 있다. 실행 코드, 전역 변수, 힙을 공유하기 때문에 여러 개의 Thread가 동시에 수정하는 경우 조심. Thread Control Block(TCB)에는 함수의 매개변수, 지역변수를 저장하는 영역을 개별적으로 가지고 있음.


# Network

## Layer
OSI 7 계층 : 물데네전세표응

![Pasted image 20231129090555](https://github.com/MadCom96/seasonallearning/assets/70102600/2294971b-ae91-4ad5-8be8-f9861b543aa5)

- 계층을 왜 나누는 것일까?
	- 단계별로 파악하여 흐름을 쉽게 알 수 있으며, 임의의 단계에서 이상이 생기면 해당 단계만 수정할 수 있다. 마치 알고리즘 코드를 작성할 때 Main함수에 전부 작성하냐 아니면 적절히 함수를 나누냐의 문제

### Protocol
절차를 포함한 통신 규약

##### Hypertext Transfer Protocol (HTTP)
HTML 문서를 주고받는데 사용하는 프로토콜
##### Transmission Control Protocol (TCP)
전송을 제어하기 위한 프로토콜이며 신뢰성 있는 통신을 위해 3-Way Handshaking, 4-Way Handshaking을 사용한다.
<img width="996" alt="Pasted image 20231129092405" src="https://github.com/MadCom96/seasonallearning/assets/70102600/dfa92e1a-4bf2-4962-9e32-b3f96b46ec12">
<img width="951" alt="Pasted image 20231129092454" src="https://github.com/MadCom96/seasonallearning/assets/70102600/317c5677-0f13-41b9-9aaa-75bec272d7b5">

3-Way Handshaking은 연결을 만들기 위해 수행
4-Way Handshaking은 연결을 해제하기 위해 수행
- TCP Reliability
	- TCP는 신뢰성을 보장하는 프로토콜이지만 패킷의 손실 순서 뒤바뀜, 네트워크 혼잡과 같은 문제를 해결해야만 한다.
##### Data Loss, Retransmission - Flow Control
**Flow Control : 송신측과 수신측의 데이터 처리 속도 차이를 해결하기 위한 기법**
- Stop and Wait
	- 데이터를 Segment로 나누어 보낸다.
	- 하나의 Segment당 하나의 ACK를 보내 서버측의 수신을 확인한다.
- Sliding Window
	- 여러개의 Segment를 Frame으로 묶어 보낸다.
	- 해당 Frame 당 하나의 ACK를 보내 서버측의 수신을 확인한다.
	- 해당 프레임(윈도우)은 수신(서버)측에서 크기를 설정하고 그 크기만큼의 데이터를 먼저 받은 후 ACK를 보내는 것.
	- 수신 윈도우의 크기보다 작거나 같은 크기로 송신 윈도우를 지정하여 흐름제어

![Pasted image 20231129093624](https://github.com/MadCom96/seasonallearning/assets/70102600/b44ca8bb-9f41-450a-83f9-3c2b7e701959)

##### Data Loss, Retransmission - Congestion Control
**Additive Intrease, Multiple Decrease (AIMD)**
최초 패킷을 하나씩 전송하고 문제가 없다면 Window Size를 1 씩 증가시켜 전송하는 방법.
전송에 실패하는 경우 전송 속도를 절반으로 줄인다.

**Slow Start**
패킷을 하나씩 전송하고 문제가 없다면 ACK 패킷마다 Window Size를 2배 씩 증가시켜주는 방법.

**Fast Retransmit**
수신 측에서 도착하지 않은 패킷이 있다면 해당 패킷의 번호를 ACK로 3 번 전송하는 방법.
송신 측에서 3 번 ACK를 받으면 곧 바로 해당 패킷을 재전송한다.


### Internet Protocol (IP)
패킷이 네트워크를 통해 목적지에 도착할 수 있도록 경로를 지정하기 위한 프로토콜.

<img width="996" alt="Pasted image 20231129094129" src="https://github.com/MadCom96/seasonallearning/assets/70102600/a3b002d5-9579-4566-bec5-71ef9293ae1d">

- Time to Live (TTL) : 패킷이 살아있는 시간 (홉 지나는 횟수, 홉 : 라우터 간의 이동)

<img width="610" alt="Pasted image 20231129094348" src="https://github.com/MadCom96/seasonallearning/assets/70102600/69910d3e-e24e-4a18-9483-8e4166bd5e61">

- Transport : TCP
- Network : IP
- Data link : MAC

##### Domain Name Server(DNS)
도메인에 맞는 IP 주소를 테이블로 갖고 있다.
www.ssafy.com 이라는 주소를 보낸다면
com : Root DNS 에서 검사
ssafy.com : Top-Level DNS에서 검사
www.ssafy.com : Second-Level DNS에서 검사
위의 검사를 모두 마치고 나온 IP 주소 112.106.xxx.xxx를 요청한 클라이언트에게 전송

##### Address Resolution Protocol (ARP)
IP 주소를 MAC 주소와  대응하기 위한 프로토콜
`arp -a` 와 같은 명령어로 현재 라우터에 연결된 노트북들의 MAC 확인 가능
- RARP : MAC -> IP


### Media Access Control (MAC)
하드웨어를 제어하는 계층으로 고유한 식별자 (MAC Address)를 가지고 있다.


## Route
##### Routing
통신하고자 하는 위치까지 어떤 경로로 이동할 것인가?
라우팅 테이블을 이용한다.
**Routing Information Protocol (RIP)**
UDP/IP 상에서 동작하는 프로토콜. Distance Vector를 기반으로 한다.
**Open Shortest Path First (OSPF)**
Link State 라우팅 알고리즘을 기반으로 하는 프로토콜.
**Border Gateway Protocol (BFP)**
Path Vector 라우팅 알고리즘을 기반으로 하는 프로토콜.

##### Routing Information Protocol (RIP)
*Distance Vector*
각 노드마다의 인접거리벡터(1차원)를 가진다.

<img width="391" alt="Pasted image 20231129101234" src="https://github.com/MadCom96/seasonallearning/assets/70102600/c7867d4b-976b-456a-913a-4d5f3c8314b4">

<img width="620" alt="Pasted image 20231129101305" src="https://github.com/MadCom96/seasonallearning/assets/70102600/b375f517-447b-4990-a5cb-09f4f6ce270d">

연결된 노드들의 테이블을 확인해서 그 비용만큼 더해가며 테이블을 갱신시킨다

##### Open Shortest Path First (OSPF)
*Link-State(Dijkstra 알고리즘 이용)*
2차원 거리벡터를 가진다.
A에서 가는 가장 짧은 거리를 선택하여 길을 fix한다.

##### Border Gateway Protocol (BFP)
*Path Vector*

<img width="755" alt="Pasted image 20231129101914" src="https://github.com/MadCom96/seasonallearning/assets/70102600/f4485689-ed54-48a3-8b65-96e048280ed6">

경로를 가진다.
기존의 경로와 이전의 경로를 합쳐 새로 갱신을 해준다.

<img width="917" alt="Pasted image 20231129101956" src="https://github.com/MadCom96/seasonallearning/assets/70102600/10a08e87-2632-4682-9bfd-db14ca2b90d1">


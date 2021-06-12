# 1. System Structure & Program Execution-1

![1%20System%20Structure%20&%20Program%20Execution-1%2018e494ea7e9c45a583d52edad4322bb2/KakaoTalk_20210612_192339617.jpg](img\System Structure&Program Execution/KakaoTalk_20210612_192339617.jpg)



---



# Mode bit

다른 프로그램 및 운영체제에 피해가 가지 않도록 하기 위한 보호장치

> bit 1: 사용자 모드 - 사용자 프로그램 수행. 제한된 인스트럭션만 수행 가능
bit 0: 모니터 모드 - OS  코드 수행. 모든 인스트럭션에 대하여 수행 가능

- 보안을 해칠 수 있는 중요한 명령어는 모니터 모드에서만 수행 가능한 '특권명령'으로 규정.
- 인터럽트가 발생 시 mode bit을 0으로 바꾸고 사용자 프로그램에게 CPU를 넘기기 전에 mode bit을 1로 세팅

**모니터모드 = 커널 모드, 시스템 모드**



# Timer

특정 프로그램의 CPU 독점을 방지하기 위해 프로그램이 CPU 사용하는 데 있어 제한시간을 측정하도록 함.

- 정해진 시간이 흐른 뒤 OS에게 제어권이 넘어가도록 인터럽트를 발생시킴
- 타이머는 매 클럭 틱 때마다 1씩 감소
- 타이머 값이 0이 되면 타이머 인터럽트 발생
- **Time Sharing(시분할 시스템)**을 구현하기 위해 널리 이용됨
- 현재 시간을 계산하기 위해서도 사용



# Device Controller

- I/O device controller
- 해당 I/O 장치유형을 관리하는 일종의 작은 CPU
- 제어 정보를 위해 control register, status register를 가짐 → 제어 데이터 저장 
- local buffer를 가짐(일종의 data register) → 데이터 저장
- I/O는 실제 Device와 local buffer 사이에서 발생
- Device controller는 I/O가 끝났을 경우 interrupt로 CPU에 그 사실을 알림

> Device driver(장치구동기): OS 코드 중 각 장치별 처리루틴 → S/W
Device controller(장치제어기): 각 장치를 통제하는 일종의 작은 CPU → H/W

* device driver의 경우 device마다 장치를 제어하기 위한 인터페이스에 맞게 접근하도록 하는 S/W임



# 입출력(I/O)의 수행

- 모든 입출력 명령은 특권 명령
- 사용자 프로그램의 I/O 과정
* 시스템콜(System Call): OS를 통해서만 제어가 가능하기에 OS의 커널 함수를 호출하여 OS에게 I/O를 요청.
* trap을 사용하여 인터럽트 벡터의 특정 위치로 이동
* 제어권이 인터럽트 벡터가 가리키는 인터럽트 서비스 루틴으로 이동
* 올바른 I/O 요청인지 확인 후 I/O 수행
* I/O 완료 시 제어권을 시스템콜 다음 명령으로 옮김 ex)H/W 인터럽트

> trap: 사용자 프로그램이 직접 인터럽트. DMA Controller를 이용해 I/O 인스트력션을 OS 대신 메모리에 적재. OS는 메모리에 올려진 인스트럭션만을 이용하여 동작 수행



# 인터럽트(Interrupt)

인터럽트 당한 시점의 레지스터와 program counter을 저장한 후 CPU의 제어를 인터럽트 처리 루틴에 넘긴다.

- Interrupt(H/W 인터럽트): 하드웨어가 발생시킨 인터럽트
- Trap(S/W 인터럽트):
- Exception: 프로그램이 오류를 범한 경우
- System call: 프로그램이 커널 함수를 호출하는 경우
- 인터럽트 처리 루틴(Interrupt Service Routine, 인터럽트 핸들러): 인터럽트를 처리하는 함수. 각 인터럽트마다 수행해야 하는 일종의 매뉴얼대로 작업 수행
- 인터럽트 벡터: 해당 인터럽트의 처리 루틴 주소: 인터럽트 처리 루틴이 저장되어 있는 일종의 주소테이블
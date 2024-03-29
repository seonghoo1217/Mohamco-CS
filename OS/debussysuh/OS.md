# 1. OS (Operating System)
---
사용자가 컴퓨터를 쉽게 다루게 해주는 인터페이스
- 한정된 메모리나 시스템 자원을 효율적으로 분배
- 하드웨어와 소프트웨어(유저 프로그램) 관리

## 1.1. 운영체제의 역할과 구조
---
역할
1. CPU 스케줄링과 프로세스 관리
	- CPU 소유권을 어떤 프로세스에 할당할지
	- 프로세스의 생성과 삭제
	- 자원 할당 및 반환 관리
2. 메모리 관리
	- 한정된 메모리를 어떤 프로세스에 얼만큼 할당해야 하는지 관리
3. 디스크 파일 관리
	- 디스크 파일을 어떠한 방법으로 보관할 지 관리
4. I/O 디바이스 관리
	- I/O 디바이스(마우스, 키보드)와 컴퓨터 간에 데이터를 주고받는 것 관리

구조
- 유저 프로그램
- 운영체제
	- GUI
	- 시스템콜
	- 커널
	- 드라이버
- 하드웨어

- GUI : 사용자가 전자장치와 상호 작용할 수 있도록 하는 사용자 인터페이스의 한 형태, 단순 명령어 창이 아닌 아이콘을 마우스로 클릭하는 단순한 동작으로 컴퓨터와 상호 작용할 수 있도록 한다.
- 드라이버 : 하드웨어를 제어하기 위한 소프트웨어
- CUI : 그래픽이 아닌 명령어로 처리하는 인터페이스
- I/O 요청 : 입출력 함수, 데이터베이스, 네트워크, 파일 접근 등에 관한 일


### 시스템콜
> 운영체제가 커널에 접근하기 위한 인터페이스
- 유저 프로그램이 운영체제의 서비스를 받기 위해 커널 함수를 호출할 때 사용
- 컴퓨터 자원에 대한 직접 접근 차단
- 프로그램을 다른 프로그램으로부터 보호

동작
- 유저 프로그램이 I/O 요청으로 트랩(trap)을 발동하면 올바른 I/O 요청인지 확인한 후 유저 모드가 시스템콜을 통해 커널 모드로 변환되어 실행된다.
- 예시
	- I/O 요청인 fs.readFile()이라는 파일 시스템의 파일 읽는 함수 발동했을 떄
		- 유저 모드에서 파일을 읽지 않고 커널 모드로 들어가 파일을 읽고 다시 유저 모드로 돌아가 그 뒤에 있는 유저 프로그램의 로직 수행


- 프로세스나 스레드에서 운영체제로 어떠한 요청을 할 때 시스템콜이라는 인터페이스와 커널을 거쳐 운영체제에 전달
- 시스템콜은 하나의 추상화 계층
	- 네트워크 통신이나 데이터베이스와 같은 낮은 단계의 영역 처리에 대한 부분을 많이 신경 쓰지 않고 프로그램을 구현할 수 있는 장점

**modebit**
> 시스템콜이 작동될 때 modebit을 참고해서 유저 모드와 커널 모드 구현
> 1 또는 0의 값을 가지는 플래그 변수

카메라, 키보드 등 I/O 디바이스는 운영체제를 통해서만 작동해야 한다. 카메라는 켜는 프로그램이 있다고 할 때, 유저 모드를 기반으로 카메라가 켜진다면 사용자가 의도하지 않았는데 공격자가 카메라를 갑자기 켤 수 있는 등 나쁜 짓을 하기 쉽다.

물론 커널 모드를 거쳐 운영체제를 통해 작동한다 해도 100% 막을 수는 없지만, 운영체제를 통해 작동하게 해야 막기 쉽다.
modebit의 0은 커널모드, 1은 유저 모드

- 유저 모드 : 유저가 접근할 수 있는 영역을 제한적으로 두며 컴퓨터 자원에 함부로 침범하지 못하는 모드
- 커널 모드 : 모든 컴퓨터 자원에 접근할 수 있는 모드
- 커널 : 운영체제의 핵심 부분이자 시스템콜 인터페이스 제공
	- 보안, 메모리, 프로세스, 파일 시스템, I/O 디바이스, I/O 요청 관리 등 운영체제의 중추적인 역할


## 1.2. 컴퓨터의 요소
---
CPU, DMA 컨트롤러, 메모리, 타이머, 디바이스 컨트롤러 등

### 1. CPU

CPU(Central Processing Unit) : 산술논리연산장치, 제어장치, 레지스터로 구성된 컴퓨터 장치
- 인터럽트에 의해 단순히 메모리에 존재하는 명령어 해석해서 실행
- 운영체제의 커널(관리자 역할)이 프로그램을 메모리에 올려 프로세스로 만들면 CPU가 처리(일꾼)

**제어장치** (CU, Control Unit)
프로세스 조작을 지시하는 CPU의 한 부품
- 입출력장치 간 통신 제어
- 명령어 읽고 해석
- 데이터 처리를 위한 순서 결정

**레지스터**
CPU 안에 있는 매우 빠른 임시기억장치
- CPU와 직접 연결되어 있어 연산 속도가 메모리보다 수십 배, 수백 배 빠름
- CPU는 자체적으로 데이터를 저장할 방법이 없기 때문에 레지스터를 거쳐 데이터 전달

**산술논리연산장치** (ALU, Arithmetic Logic Unit)
덧셈, 뺄셈 같은 두 숫자의 산술 연산과 배타적 논리합, 논리곱 같은 논리 연산을 계산하는 디지털 회로
- CPU의 연산 처리
	- CPU에서 제어장치, 레지스터, 산술논리연산장치를 통해 연산하는 예
		1. 제어장치가 메모리와 레지스터에 계산할 값 로드
		2. 제어장치가 레지스터에 있는 값을 계산하라고 산술논리연산장치에 명령
		3. 제어장치가 계산된 값을 다시 '레지스터에서 메모리로' 계산한 값 저장


**인터럽트** 
어떤 신호가 들어왔을 때 CPU를 잠깐 정지시키는 것
- 종류
	- 하드웨어 인터럽트
		- 키보드나 마우스 연결하는 일 등의 IO 디바이스에서 발생하는 인터럽트
		- 인터럽트 라인이 설계된 이후 순차적인 인터럽트 실행 중지 -> 운영체제에 시스템콜 요청 -> 원하는 디바이스로 향해 디바이스에 있는 작은 로컬 버퍼에 접근하여 일 수행
	- 소프트웨어 인터럽트
		- 트랩(trap)이라고도 한다.
		- 프로세스 오류 등으로 프로세스가 시스템콜을 호출할 때 발동
- 키보드, 마우스 등 IO 디바이스로 인한 인터럽트
- 0으로 숫자를 나누는 산술 연산에서의 인터럽트
- 프로세스 오류

인터럽트가 발생되면 인터럽트 핸들러 함수가 모여 있는 인터럽트 벡터로 가서 인터럽트 핸들러 함수 실행
인터럽트 간에는 우선순위가 있고, 우선순위에 따라 실행된다.

- 인터럽트 핸들러 함수
	- 인터럽트가 발생했을 때 이를 핸들링하기 위한 함수
	- 커널 내부의 IRQ를 통해 호출된다.
	- request_irq()를 통해 인터럽트 핸들러 함수 등록 가능


### 2. DMA 컨트롤러
: I/O 디바이스가 메모리에 직접 접근할 수 있도록 하는 하드웨어 장치 (CPU의 일 부담하는 보조 일꾼)
- CPU에만 너무 많은 인터럽트 요청이 들어오기 때문에 CPU 부하를 막아 준다.
- 하나의 작업을 CPU와 DMA 컨트롤러가 동시에 하는 것 방지


### 3. 메모리 (Memory)
: 전자회로에서 데이터나 상태, 명령어 등을 기록하는 장치
보통 RAM(random Access Memory)을 일컬어 메모리라고도 한다.
- CPU - 계산 담당, Memory - 기억 담당
- 메모리가 크면 클수록 많은 일을 동시에 가능


### 4. 타이머 (Timer)
: 몇 초 안에는 작업이 끝나야 한다는 것을 정하고 특정 프로그램에 시간 제한을 다는 역할
시간이 많이 걸리는 프로그램이 작동할 때 제한을 걸기 위해 존재


### 5. 디바이스 컨트롤러 (Device Controller)
: 컴퓨터와 연결되어 있는 IO 디바이스들의 작은 CPU를 말한다.
- 옆에 붙어 있는 로컬 버퍼
	- 각 디바이스에서 데이터를 임시로 저장하기 위한 작은 메모리





# 2. 메모리
---
CPU는 그저 메모리에 올라와 있는 프로그램의 명령어를 실행할 뿐이다.

## 2.1. 메모리 계층
---
- **램 (RAM)** : 하드디스크로부터 일정량의 데이터를 복사해서 임시 저장하고 이를 필요 시마다 CPU에 빠르게 전달하는 역할
- 계층 위로 올라갈수록 가격은 비싸지며 용량은 적어지고 속도는 빨라지는 특징
	- 그 이유는 경제성과 캐시 때문에 계층을 두어 관리한다.
+ 게임의 '로딩 중' 메시지 : 하드디스크 또는 인터넷에서 데이터를 읽어 RAM으로 전송하는 과정이 아직 끝나지 않았음을 의미

![[Pasted image 20230128012731.png]]
- 레지스터 : CPU 안에 있는 작은 메모리
	- 휘발성, 속도 가장 빠름, 기억 용량 가장 적음
- 캐시 : L1, L2 캐시 지칭 (L3 캐시도 존재)
	- 휘발성, 속도 빠름, 기억 용량 적음
- 주기억장치 : 메모리(RAM) 지칭
	- 휘발성, 속도 보통, 기억 용량 보통
- 보조기억장치 : 저장장치(HDD, SSD) 지칭
	- 비휘발성, 속도 낮음, 기억 용량 많음(높음)


### 캐시 (cache)
---

> 데이터를 미리 복사해 놓는 임시 저장소

빠른 장치와 느린 장치에서 속도 차이에 다른 병목 현상을 줄이기 위한 메모리
- 데이터를 접근하는 시간이 오래 걸리는 경우 해결하여 무언가 다시 계산하는 시간 절약 가능
- 캐싱 계층
	- 메모리와 CPU 사이의 속도 차가 너무 크기 때문에 그 중간에 레지스터 계층을 둬서 속도 차이 해결
	- 캐시 메모리와 보조기억장치 사이에 있는 주기억장치를 보조기억장치의 캐싱 계층이라고 한다.


**지역성의 원리**
> 캐시 계층을 두는 것 말고 캐시를 직접 설정할 때는 어떻게 해야 할까?
> 이는 자주 사용하는 데이터를 기반으로 설정해야 한다.
> 그렇다면 자주 사용하는 데이터에 대한 근거가 되는 것은 무엇일까?
> 바로 지역성이다.

지역성
- 시간 지역성 (temporal locality)
	- 최근 사용한 데이터에 다시 접근하려는 특성
- 공간 지역성 (spatial locality)
	- 최근 접근한 데이터를 이루고 있는 공간이나 그 가까운 공간에 접근하는 특성



### 캐시히트, 캐시미스
---

캐시히트 :  캐시에서 원하는 데이터를 찾음
	- 캐시히트를 하게 되면, 해당 데이터를 제어장치에 거쳐 가져오게 된다.
	- 위치도 가까워 CPU 내부 버스를 기반으로 작동하므로 빠르다.
캐시미스 : 해당 데이터가 캐시에 없다면 주 메모리로 가서 데이터를 찾아오는 것
	- 캐시미스가 발생되면, 메모리에서 가져오게 된다.
	- 시스템 버스를 기반으로 작동하므로 느리다.

**A. 캐시매핑**
: 캐시가 히트되기 위해 매핑하는 방법
- CPU의 레지스터와 주 메모리(RAM) 간에 데이터를 주고받을 때를 기반으로 설명
- 레지스터는 주 메모리에 비하면 굉장히 작고, 주 메모리는 굉장히 크다.
	- 작은 레지스터가 캐시 계층으로써 역할을 잘 해주려면 이 매핑을 어떻게 하느냐가 중요하다.

분류
- 직접 매핑 (directed mapping)
	- 메모리가 1~100이 있고 캐시가 1~10이 있다면, 1:1~10, 2:1~20.. 이런 식의 매핑 방식
	- 처리가 빠르나 충돌 발생이 잦다.
- 연관 매핑 (associative mapping)
	- 순서를 일치시키지 않고 관련 있는 캐시와 메모리를 매핑한다.
	- 충돌이 적으나 모든 블록을 탐색해야 하므로 속도가 느리다.
- 집합 연관 매핑 (set associative mapping)
	- 직접 매핑 + 연관매핑
	- 순서는 일치시키지만 집합을 둬서 저장한다.
	- 블록화되어 있어 검색은 좀 더 효율적
	- 메모리가 1~100이 있고 캐시가 1~10이 있다면, 캐시 1~5에는 1~50의 데이터를 무작위로 저장시키는 것을 말한다.


**B. 웹 브라우저의 캐시**
보통 사용자의 커스텀한 정보나 인증 모듈 관련 사항들을 웹 브라우저에 저장해서 추후 서버에 요청할 때 자신을 나타내는 아이덴티티나 중복 요청 방지를 위해 쓰인다.

**1. 쿠키**
> 만료기한이 있는 키-값 저장소
- same site 옵션을 strict로 설정하지 않았을 경우 다른 도메인에서 요청했을 때 자동 전송된다.
- 4KB까지 데이터 저장, 만료기한 정하기 가능
- 쿠키 설정 시, document.cookie로 쿠키를 볼 수 없게 httponly 옵션을 걸어야 한다.
- 클라이언트 또는 서버에서 만료기한 등을 정할 수 있는데 보통 서버에서 만료기한을 정한다.

**2. 로컬 스토리지**
> 만료기한이 없는 키-값 저장소
- 10MB까지 저장 가능
- 웹 브라우저를 닫아도 유지되며 도메인 단위로 저장, 생성된다.
- HTML5를 지원하지 않는 웹 브라우저에서 사용 불가
- 클라이언트에서만 수정 가능

**3. 세션 스토리지** 
> 만료기한이 없는 키-값 저장소
- 탭 단위로 세션 스토리지 생성, 탭 닫을 때 해당 데이터 삭제된다.
- 5MB까지 저장 가능
- HTML5를 지원하지 않는 웹 브라우저에서 사용 불가
- 클라이언트에서만 수정 가능


**C. 데이터베이스의 캐싱 계층**
데이터베이스 시스템을 구축할 때도 메인 데이터베이스 위에 레디스(redis) 데이터베이스 계층을 '캐싱 계층'으로 둬서 성능을 향상시키기도 한다.
- 캐시히트: 레디스로부터 데이터를 읽어온다.
- 캐시미스: 메인 데이터베이스로부터 데이터를 가져온다.
- 데이터를 레디스에 쓴다.




## 2.2. 메모리 관리
---
운영체제의 대표적인 할 일 중 하나인 메모리 관리
컴퓨터 내의 한정된 메모리를 극한으로 활용해야 한다.

### 1. 가상 메모리 (virtual memory)
---

> 컴퓨터가 실제로 이용 가능한 메모리 자원을 추상화하여 이를 사용하는 사용자들에게 매우 큰 메모리로 보이게 만드는 것

![[Pasted image 20230128235009.png]]
가상 주소는 메모리관리장치(MMU)에 의해 실제 주소로 변환되며, 이 덕분에 사용자는 실제 주소를 의식할 필요 없이 프로그램을 구축할 수 있게 된다.
- 가상 주소 (logical address) : 가상적으로 주어진 주소
- 실제 주소 (physical address) : 실제 메모리상에 있는 주소

**특징**
- 가상 주소와 실제 주소가 매핑되어 있다.
- 프로세스의 주소 정보가 들어 있는 '페이지 테이블'로 관리된다.
- 이때 속도 향상을 위해 TLB를 쓴다.
	- TLB : 메모리와 CPU 사이에 있는 주소 변환을 위한 캐시
		- 페이지 테이블에 있는 리스트를 보관하며 CPU가 페이지 테이블까지 가지 않도록 해 속도를 향상시킬 수 있는 캐시 계층


**스와핑**
만약 가상 메모리에는 존재하지만 실제 메모리인 RAM에는 현재 없는 데이터나 코드에 접근할 경우 '페이지 폴트'가 발생한다. 이때 메모리에서 당장 사용하지 않는 영역을 하드디스크로 옮기고 **하드디스크의 일부분을 마치 메모리처럼 불러와 쓰는 것**을 말한다.

**페이지 폴트 (page fault)**
프로세스의 주소 공간에는 존재하지만 지금 이 컴퓨터의 RAM에는 없는 데이터에 접근했을 경우에 발생한다.

- 페이지 폴트와 그로인한 스와핑이 이루어지는 과정
	1. CPU는 물리 메모리를 확인하여 해당 페이지가 없으면 트랩을 발생해서 운영체제에 알린다.
	2. 운영체제는 CPU의 동작을 잠시 멈춘다.
	3. 운영체제는 페이지 테이블을 확인하여 가상 메모리에 페이지가 존재하는지 확인하고, 없으면 프로세스를 중다하고 현재 물리 메모리에 비어 있는 프레임이 있는지 찾는다. 물리 메모리에도 없다면 스와핑이 발동된다.
	4. 비어 있는 프레임에 해당 페이지를 로드하고, 페이지 테이블을 최신화한다.
	5. 중단되었던 CPU를 다시 시작한다.
- 페이지 (page) : 가상 메모리를 사용하는 최소 크기 단위
- 프레임 (frame) : 실제 메모리를 사용하는 최소 크기 단위


### 2. 스레싱 (thrashing)
---

> 메모리의 페이지 폴트율이 높은 것을 의미
> 이는 컴퓨터의 심각한 성능 저하를 초래한다.
> 메모리에 너무 많은 프로세스가 동시에 올라가게 되면 스와핑이 많이 일어나 발생한다.

![[Pasted image 20230129000900.png]]
**스레싱이 일어나는 과정**
- 페이지 폴트 발생 -> CPU 이용률 낮아짐 -> 운영체제가 더 많은 프로세스를 메모리에 올림 ->  반복
페이지 폴트가 일어나면 CPU 이용률이 낮아진다. CPU 이용률이 낮아지게 되면 운영체제는 'CPU가 한가한가?'라고 생각하여 가용성을 더 높이기 위해 더 많은 프로세스를 메모리에 올리게 된다. 이와 같은 악순환이 반복되며 스레싱이 일어나게 된다.

**해결 방법**
- 메모리를 늘린다.
- HDD를 사용하여 HDD->SSD로 바꾼다.
- 작업 세트
- PFF

**작업 세트 (working set)**
프로세스의 과거 사용 이력인 지역성(locality)을 통해 결정된 페이지 집합을 만들어서 미리 메모리에 로드하는 것
- 미리 메모리에 로드하면 탐색에 드는 비용 절감 가능
- 스와핑 줄이기 가능

**PFF (Page Fault Frequency)**
페이지 폴트 빈도를 조절하는 방법으로, 상한선과 하한선을 만든다.
- 만약 상한선에 도달한다면 프레임을 늘린다.
- 하한선에 도달한다면 프레임을 줄인다.


### 3. 메모리 할당
---

> 메모리에 프로그램을 할당할 때는 시작 메모리 위치, 메모리의 할당 크기를 기반으로 할당하는데, 연속 할당과 불연속 할당으로 나뉜다.

**A. 연속 할당**
: 메모리에 '연속적으로' 공간을 할당하는 것
예를 들어 프로세스 a, b, c가 순차적으로 공간에 할당하는데, 이는 메모리를 미리 나누어 관리하는 고정 분할 방식과 매 시점 프로그램의 크기에 맞게 메모리를 분할하여 사용하는 가변 분할 방식이 있다.

**고정 분할 방식 (fixed partition allocation)**
메모리를 미리 나누어 관리하는 방식
- 메모리가 미리 나뉘어 있기 때문에 융통성이 없다.
- 내부 단편화 발생

**가변 분할 방식 (variable partition allocation)**
매 시점 프로그램의 크기에 맞게 동적으로 메모리를 나눠 사용하는 방식
- 내부 단편화 발생 X
- 외부 단편화 발생 할 수 있다.
- 종류
	- 최초적합 (first fit) : 위쪽이나 아래쪽부터 시작해서 홀을 찾으면 바로 할당한다.
	- 최적적합 (best fit) : 프로세스의 크기 이상인 공간 중 가장 작은 홀부터 할당한다.
	- 최악적합 (worst fit) : 프로세스의 크기와 가장 많이 차이가 나는 홀에 할당한다.

- 내부 단편화 (internal fragmentation)
	- 메모리를 나눈 크기보다 프로그램이 '작아서' 들어가지 못하는 공간이 많이 발생하는 현상
- 외부 단편화 (external fragmentation)
	- 메모리를 나눈 크기보다 프로그램이 '커서' 들어가지 못하는 공간이 많이 발생하는 현상
	- 100MB, 55MB, 45MB로 나눴지만 프로그램의 크기는 70MB일 때 들어가지 못하는 것
- 홀 (hole) : 할당할 수 있는 비어 있는 메모리 공간


**B. 불연속 할당**
: 메모리를 연속적으로 할당하지 않는 것
메모리를 동일한 크기의 페이지(보통 4KB)로 나누고 프로그램마다 페이지 테이블을 두어 이를 통해 메모리에 프로그램을 할당한다.
페이징 기법, 세그멘테이션, 페이지드 세그멘테이션이 있다.

**페이징 (paging)**
: 동일한 크기의 페이지 단위로 나눠 메모리의 서로 다른 위치에 프로세스를 할당한다.
- 홀의 크기가 균일하지 않은 문제 해결
- 주소 변환이 복잡해진다.

**세그멘테이션 (segmentation)**
: 페이지 단위가 아닌 의미 단위인 세그먼트로 나누는 방식
- 프로세스를 이루는 메모리는 코드 영역, 데이터 영역, 스택 영역, 힙 영역으로 이루어지는데, 코드와 데이터로 나누거나 코드 내의 작은 함수를 세그먼트로 놓고 나눌 수 있다.
- 공유와 보안 측면에서 장점을 가진다.
- 홀 크기가 균일하지 않다.

**페이지드 세그멘테이션 (paged segmentation)**
: 프로그램을 의미 단위인 세그먼트로 나누는 방식
- 임의의 길이가 아닌 동일한 크기의 페이지 단위로 나눈다.
- 공유나 보안 측면에 강점을 둔다.


### 4. 페이지 교체 알고리즘
---
메모리는 한정되어 있기 때문에 스와핑이 많이 일어난다. 스와핑은 많이 일어나지도 않도록 설계되어야 하며, 이는 페이지 교체 알고리즘을 기반으로 스와핑이 일어난다.

**오프라인 알고리즘 (offline algorithm)**
> 먼 미래에 참조되는 페이지와 현재 할당하는 페이지를 바꾸는 알고리즘

미래에 사용되는 프로세스를 우리가 알 수 없다. 즉, 사용할 수 없는 알고리즘이지만 가장 좋은 알고리즘이기 때문에 다른 알고리즘과의 성능 비교에 대한 상한기준 (upper_bound)을 제공한다.

**FIFO (First In First Out)**
가장 먼저 온 페이지를 교체 영역에 가장 먼저 놓는 방법

**LRU (Least Recentle Used)**
참조가 가장 오래된 페이지를 바꾸는 방법
- '오래된' 것을 파악하기 위해 각 페이지마다 계수기, 스택을 두어야 하는 문제점이 있다.
![[Pasted image 20230129005853.png]]
- 보통 두 개의 자료 구조로 구현
	- 해시 테이블 (이중 연결 리스트에서 빠르게 찾을 수 있도록 쓴다.)
		- unordered_map으로 구현 가능
	- 이중 연결 리스트 (한정된 메모리를 나타낸다.)
		- list로 구현 가능
		- 

```
#include <bits/stdc++.h>
using namespace std;

class LRUache {
	list<int> li;
	unordered_map<int, list<int>::iterator> hash;
	int csize;

public:
	LRUache(int);
	void refer(int);
	void display();
};

LRUache::LRUache(int n){
csize = n;
}

void LRUache::refer(int x){
	if (hash.find(x) == hash.end()) {
		if (li.size() == csize) {
		// 가장 끝에 있는 것을 뽑아낸다.
		// 이는 가장 오래된 것을 의미한다.
		int last = li.back();
		li.pop_back();
		hash.erase(last);
		}
	} else {
		li.erase(hash[x]);
	}
	// 해당 페이지를 참조할 때
	// 가장 앞에 붙인다. 또한 이를 해시 테이블에 저장한다.
	li.push_front(x);
	hash[x] = li.begin();
}

void LRUache::display() {
	for (auto it = li.begin(); it != li.end(); it++) {
	cout << (*it) << " ";
	}
	cout << "/n";
}

int main() {
	LRUache ca(3);
	ca.refer(1);
	ca.display();
	ca.refer(3);
	ca.display();
	ca.refer(0);
	ca.display()
	ca.refer(3);
	ca.display();
	ca.refer(5);
	ca.display();
	ca.refer(6);
	ca.display();
	ca.refer(3);
	ca.display();

	return 0;
}

/*
1
3 1
0 3 1
3 0 1
5 3 0
6 5 3
3 6 5
*/
```


**NUR** (Not Used Recently)
LRU에서 발전한 알고리즘으로, clock 알고리즘이라고 한다.
먼저 0과 1을 가진 비트를 둔다. 1은 최근에 참조되었고 0은 참조되지 않았음을 의미한다.
시계 방향으로 돌면서 0을 찾고 0을 찾은 순간 해당 프로세스를 교체하고, 해당 부분을 1로 바꾼다.

**LFU (lease Frequently Used)**
가장 참조 횟수가 적은 페이지 교체 즉, 많이 사용되지 않는 것을 교체한다.





# 3. 프로세스와 스레드
---
> 프로세스(process) : 컴퓨터에서 실행되고 있는 프로그램, CPU 스케줄링의 대상이 되는 작업(task)과 거의 같은 의미로 쓰인다.
> 
> 스레드 : 프로세스 내 작업의 흐름

- 프로그램이 메모리에 올라가면 프로세스가 되는 인스턴스화가 일어난다.
- 이후 운영체제의 CPU 스케줄러에 따라 CPU가 프로세스를 실행한다.


### 3.1. 프로세스와 컴파일 과정
---
- 프로세스 : 프로그램이 메모리레 올라가 인스턴스화가 된 것
	- 예를 들어, 프로그램은 구글 크롬 프로그램(chrome.exe)과 같은 실행 파일이며, 이를 두 번 클릭하면 쿠글 크롬 프로세스로 변환되는 것

프로그램을 만드는 과정은 만드는 언어마다 다를 수 있다. 컴파일 언어인 C언어 기반의 프로그램 기준으로는, 컴파일러가 컴파일 과정을 통해 컴퓨터가 이해할 수 있는 기계어로 번역하여 실행할 수 있는 파일을 만들게 된다.

**컴파일 과정**
![[Pasted image 20230129013203.png]]
- 전처리 : 소스 코드의 주석 제거, #include 등 헤더 파일을 병합하여 매크로를 치환한다.
- 컴파일러 : 오류 처리, 코드 최적화 작업, 어셈블리어로 변환
- 어셈블러 : 어셈블리어는 목적 코드로 변환된다. 이때 확장자는 운영체제마다 다른데 리눅스는 .o이다. (파일.c 생성 -> 파일.o)

**링커**
프로그램 내에 있는 라이브러리 함수 도는 다른 파일들과 목적 코드를 결합하여 실행 파일을 만든다.
실행 파일의 확장자 : .exe / .out

**라이브러리**
- 정적 라이브러리
	- 프로그램 빌드 시 라이브러리가 제공하는 모든 코드를 실행 파일에 넣는 방식
	- 장점 : 시스템 환경 등 외부 의존도가 낮다.
	- 단점 : 코드 중복 등 메모리 효율성이 떨어진다.
- 동적 라이브러리
	- 프로그램 실행 시 필요할 때만 DLL이라는 함수 정보를 통해 참조하는 방식
	- 장점 : 메모리 효율성 증가
	- 단점 : 외부 의존도가 높아진다.


### 3.2. 프로세스의 상태
---
프로세스의 상태는 여러 가지 상태 값을 갖는다.

![[Pasted image 20230129013718.png]]
1. 생성 상태 (create)
	- 프로세스가 생성된 상태
	- fork() 또는 exec() 함수를 통해 생성
	- 이때 PCB가 할당된다.
		- fork() : 부모 프로세스의 주소 공간을 그대로 복사하며, 새로운 자식 프로세스 생성하는 함수이다. 주소 공간만 복사할 뿐, 부모 프로세스의 비동기 작업 등을 상속하지 않는다.
		- exec() : 새롭게 프로세스를 생성하는 함수
		- PCB : 프로세스에 대한 메타데이터를 저장한 데이터

2. 대기 상태 (ready)
	- 메모리 공간이 충분하면 메모리를 할당받고, 아니면 아닌 상태로 대기 한다.
	- CPU 스케줄러로부터 CPU 소유권이 넘어오기를 기다리는 상태

3. 대기 중단 상태 (ready suspended)
	- 메모리 부족으로 일시 중단된 상태

4. 실행 상태 (running)
	- CPU 소유권과 메모리를 할당받고 인스트럭션을 수행 중인 상태
	- CPU burst가 일어났다고도 한다.

5. 중단 상태 (blocked)
	- 어떤 이벤트가 발생한 이후 기다리며 프로세스가 차단된 상태
	- I/O 디바이스에 의한 인터럽트로 이런 현상이 많이 발생

6. 일시 중단 상태 (blocked suspended)
	- 대기 중단과 유사
	- 중단된 상태에서 프로세스가 실행되려고 했지만 메모리 부족으로 일시 중단된 상태

7. 종료 상태 (terminated)
	- 메모리와 CPU 소유권을 모두 놓고 가는 상태
	- 자연스럽게 종료되는 것도 있고, 부모 프로세스가 자식 프로세스를 강제시키는 비자발적 종료 (abort)로 종료되는 것도 있다.
	- 자식 프로세스에 할당된 자원의 한계치를 넘어서거나, 부모 프로세스가 종료되거나, 사용자가 process.kill 등 여러 명령어로 프로세스를 종료할 때 발생


### 3.3. 프로세스의 메모리 구조
---
OS는 프로세스에 적절한 메모리를 할당하는데 다음 구조를 기반으로 할당한다.


![[Pasted image 20230129014530.png]]
- 정적 영역 : 데이터 영역(BSS segment, Data segment), 코드 영역(code segment)
- 동적 영역 : 스택(stack), 힙(heap)
	- 둘 다 동적 할당이 된다.
	- 스택 : 위 주소부터 할당된다.
	- 힙 : 아래 주소부터 할당된다.
	- 동적 할당 : 런타임 단계에서 메모리를 할당받는 것


**스택**
: 지역 변수, 매개변수, 실행되는 함수에 의해 늘어들거나 줄어드는 메모리 영역
- 함수가 호출될 때마다 호출될 때의 환경 등 특정 정보가 스택에 계속해서 저장된다.
- 재귀 함수가 호출된다고 했을 때, 새로운 스택 프레임이 매번 사용되기 때문에 함수 내의 변수 집합이 해당 함수의 다른 인스턴스 변수를 방해하지 않는다.

**힙**
: 동적으로 할당되는 변수들을 담는다.
- malloc(), free() 함수를 통해 관리
- 동적으로 관리되는 자료 구조의 경우 힙 영역 사용
	- 예를 들어, vector는 내부적으로 힙 영역 사용


**데이터 영역과 코드 영역**
- 정적 할당되는 영역
- 데이터 영역 : BSS segment와 Data segment, code/text segment로 나뉘어 저장된다.
- 코드 영역 : 컴파일 단계에서 메모리를 할당하는 것

- BSS segment : 전역 변수 또는 static, const로 선언되어 있다.
	- 0으로 초기화 또는 초기화가 어떠한 값으로도 되어 있지 않은 변수들이 이 메모리 영역에 할당된다.
- Data segment : 전역 변수 또는 static, const로 선언되어 있다.
	- 0이 아닌 값으로 초기화된 변수가 이 메모리 영역에 할당된다.
- code segment : 프로그램의 코드가 들어간다.


### 3.4. PCB
---
> PCB (Process Control Block) : 운영체제에서 프로세스에 대한 메타데이터를 저장한 데이터
> == 프로세스 제어 블록
> 프로세스가 생성되면 OS는 해당 PCB를 생성한다.
> 프로세스 스케줄링 상태, 프로세스 ID 등의 정보로 이루어져있다.

프로세스 실행 시, 프로세스 생성됨 -> 프로세스 주소 값들에 메모리가 할당됨 (스택, 힙 등의 구조 기반) -> 이 프로세스의 메타데이터들이 PCB에 저장되어 관리됨
- 프로세스의 중요한 정보를 포함하고 있기 때문에 일반 사용자가 접근하지 못하도록 커널 스택의 가장 앞부분에서 관리한다.
- 메타데이터 : 데이터에 관한 구조화된 데이터이자, 데이터를 설명하는 작은 데이터이다. 대량의 정보 가운데에서 찾고 있는 정보를 효율적으로 찾아내서 이용하기 위해 일정한 규칙에 따라 콘텐츠에 대해 부여되는 데이터이다.

**PCB의 구조**
- 프로세스 스케줄링 상태
	- '준비', '일시중단' 등 프로세스가 CPU에 대한 소유권을 얻은 이후의 상태
- 프로세스 ID
	- 프로세스 ID, 해당 프로세스의 자식 프로세스 ID
- 프로세스 권한
	- 컴퓨터 자원 또는 I/O 디바이스에 대한 권한 정보
- 프로그램 카운터
	- 프로세스에서 실행해야 할 다음 명령어의 주소에 대한 포인터
- CPU 레지스터
	- 프로세스를 실행하기 위해 저장해야 할 레지스터에 대한 정보
- CPU 스케줄링 정보
	- CPU 스케줄러에 의해 중단된 시간 등에 대한 정보
- 계정 정보
	- 프로세스 실행에 사용된 CPU 사용량, 실행한 유저의 정보
- I/O 상태 정보
	- 프로세스에 할당된 I/O 디바이스 목록


**컨텍스트 스위칭 (context switching)**
> PCB를 교환하는 과정
> 한 프로세스에 할당된 시간이 끝나거나 인터럽트에 의해 발생한다.

컴퓨터는 많은 프로그램을 동시에 실행하는 것처럼 보이지만 어떠한 시점에서 실행되고 있는 프로세스는 단 한 개이다. (싱글코어 기준)
많은 프로세스가 동시에 구동되는 것처럼 보이는 것은 다른 프로세스와의 컨텍스트 스위칭이 아주 빠른 속도로 실행되기 때문이다. 

![[Pasted image 20230130020134.png]]
한 개의 프로세스 P0가 실행하다 멈춤 -> 프로세스 P0의 PCB 저장 -> 다시 프로세스 P1를 로드하여 실행 -> 그리고 다시 프로세스 P1의 PCB를 저장 -> 프로세스 P0의 PCB 로드

컨텍스트 스위칭이 일어날 때 유휴 시간(idle time)이 발생한다.
컨텍스트 스위칭에 캐시미스 비용 발생

**비용: 캐시미스**
컨텍스트 스위칭이 일어날 때 프로세스가 가지고 있는 메모리 주소가 그대로 있으면 잘못된 주소 변환이 생기므로 캐시클리어 과정을 겪게 되고, 이 때문에 캐시미스가 발생한다.

**스레드에서의 컨텍스트 스위칭**
컨텍스트 스위칭은 스레드에서도 일어난다. 스레드는 스택 영역을 제외한 모든 메모리를 공유하기 때문에 스레드 컨텍스트 스위칭의 경우 비용이 더 적고 시간도 더 적게 걸린다.



### 3.5. 멀티프로세싱
---
> 여러 개의 '프로세스' 즉, 멀티프로세스를 통해 동시에 두 가지 이상의 일을 수행할 수 있는 것
> 이를 통해 하나 이상의 일을 병렬로 처리할 수 있다.

- 특정 프로세스의 메모리, 프로세스 중 일부에 문제가 발생되더라도 다른 프로세스를 이용해서 처리할 수 있으므로 신뢰성이 높다.

**웹 브라우저**
웹 브라우저는 멀티프로세스 구조를 가지고 있다.
- 브라우저 프로세스
	- 주소 표시줄, 북마크 막대, 뒤로 가기 버튼, 앞으로 가기 버튼 등 담당
	- 네트워크 요청, 네트워크 통신이나 파일 접근 같은 권한 담당
- 렌더러 프로세스
	- 웹 사이트가 '보이는' 부분의 모든 것을 제어
- 플러그인 프로세스
	- 웹 사이트에서 사용하는 플러그인 제어
- GPU 프로세스
	- GPU를 이용해서 화면을 그리는 부분 제어


**IPC (Inter Process Communication)**
> IPC는 프로세스끼리 데이터를 주고받고 공유 데이터를 관리하는 메커니즘
> 멀티프로세스는 IPC가 가능하다.

IPC의 예
- 클라이언트와 서버 : 클라이언트 - 데이터 요청, 서버 - 클라이언트 요청에 응답

IPC 종류
: 모두 메모리가 완전히 공유되는 스레드보다는 속도가 떨어진다.
1. 공유 메모리 (shared memory)
	- 여러 프로세스에 동일한 메모리 블록에 대한 접근 권한이 부여되어 프로세스가 서로 통신할 수 있도록 공유 메모리를 생성해서 통신하는 것
2. 파일
	- 디스크에 저장된 데이터 또는 파일 서버에서 제공한 데이터
	- 이를 기반으로 프로세스 간 통신을 한다.
3. 소켓
	- 동일한 컴퓨터의 다른 프로세스나 네트워크의 다른 컴퓨터로 네트워크 인터페이스를 통해 전송하는 데이터
	- TCP, UDP
4. 익명 파이프 (unamed pipe)
	- 프로세스 간에 FIFO 방식으로 읽히는 임시 공간인 파이프를 기반으로 데이터를 주고받는다.
	- 단방향 방식의 읽기 전용, 쓰기 전용 파이프를 만들어서 작동
	- 부모, 자식 프로세스 간에만 사용 가능
	- 다른 네트워크상에서는 사용 불가
5. 명명 파이프 (named pipe)
	- 파이프 서버와 하나 이상의 파이프 클라이언트 간의 통신을 위한 명명된 단방향, 양방향 파이프
6. 메시지 큐
	- 메시지를 큐 데이터 구조 형태로 관리하는 것




**공유 메모리**
- 기본적으로 각 프로세스의 메모리를 다른 프로세스가 접근할 수 없지만 공유 메모리를 통해 여러 프로세스가 하나의 메모리를 공유할 수 있다.
- 속도 빠름 : IPC 방식 중 어떠한 매개체를 통해 데이터를 주고받는 것이 아닌 메모리 자체를 공유하기 때문에 불필요한 데이터 복사의 오버헤드가 발생하지 않아 가장 빠르다.
- 동기화 필요 : 같은 메모리 영역을 여러 프로세스가 공유하기 때문에 동기화가 필요하다.


**명명 파이프**
- 클라이언트/서버 통신을 위한 별도의 파이프 제공
- 여러 파이프 동시 사용 가능
- 컴퓨터의 프로세스끼리 또는 다른 네트워크상의 컴퓨터와 통신 가능
- 보통 서버용 파이프와 클라이언트용 파이프로 구분해서 작동
- 하나의 인스턴스를 열거나 여러 개의 인스턴스를 기반으로 통신


**메시지 큐**
- 커널의 전역변수 형태 등 커널에서 전역적으로 관리된다.
- 다른 IPC 방식에 비해 사용 방법이 매우 직관적, 간단
- 다른 코드의 수정 없이 단지 몇 줄의 코드를 추가시켜 간단하게 메시지 큐에 접근 가능
- 공유 메모리 동기화 문제 대안 : 공유 메모리를 통해 IPC를 구현할 때 쓰기 및 읽기 빈도가 높으면 동기화 때문에 기능을 구현하는 것이 매우 복잡해진다. 이때 대안으로 메시지 큐를 사용하기도 한다.



### 3.6. 스레드와 멀티스레딩
---

**스레드**
> 프로세스에 의해 실행 가능한 가장 작은 단위

프로세스는 여러 스레드를 가질 수 있다.
![[Pasted image 20230130023023.png]]
- 프로세스 - 코드, 데이터, 스택, 힙을 각각 생성
- 스레드 - 코드, 데이터, 힙은 스레드끼리 서로 공유, 그 외 영역 각각 생성


**멀티스레딩**
> 프로세스 내 작업을 여러 개의 스레드, 멀티스레드로 처리하는 기법

장점
- 효율성 : 스레드끼리 서로 자원을 공유하기 때문에 효율성이 높다.
- 동시성
	- 서로 독립적인 작업들을 작은 단위로 나누고 동시에 실행되는 것처럼 보여주는 것
- 웹 요청을 처리할 때 새 프로세스를 생성하는 대신, 스레드를 사용하는 웹 서버의 경우
	- 훨씬 적은 리소스 소비, 한 스레드가 중단(blocked)되어도 다른 스레드는 실행(running) 상태일 수 있기 때문에 중단되지 않은 빠른 처리 가능

단점
- 한 스레드에 문제가 생기면 다른 스레드에도 영향을 끼쳐 스레드로 이루어져 있는 프로세스에 영향을 줄 수 있다.

예
: 웹 브라우저의 렌더러 프로세스를 이루는 스레드
- 이 프로세스 내에는 메인 스레드, 워커 스레드, 컴포지터 스레드, 레스티 스레드 존재



### 3.7. 공유 자원과 임계 영역
----

**공유 자원 (shared resource)**
> 시스템 안에서 각 프로세스, 스레드가 함께 접근할 수 있는 모니터, 프린터, 메모리, 파일, 데이터 등의 자원이나 변수 등

경쟁 상태 (race condition)
: 공유 자원을 두 개 이상의 프로세스가 동시에 읽거나 쓰는 상황
- 동시에 접근을 시도할 때 접근의 타이밍이나 순서 등이 결괏값에 영향을 줄 수 있는 상태

![[Pasted image 20230130024109.png]]
종선 코인 100개가 있다고 할 때, 프로세스 A와 프로세스 B가 동시에 접근하여 타이밍이 서로 꼬여 정상 결괏값은 300인데 200이 출력된다.


**임계 영역(critical section)**
> 둘 이상의 프로세스, 스레드가 공유 자원에 접근할 때 순서 등의 이유로 결과가 달라지는 코드 영역

**임계 영역을 해결하기 위한 방법**
1. 뮤텍스 (mutex)
2. 세마포어 (semaphore)
3. 모니터
이 방법 모두 상호 배제, 한정 대기, 융통성이란 조건 만족
- 상호 배제 : 한 프로세스가 임계 영역에 들어갔을 때 다른 프로세스는 들어갈 수 없다.
- 한정 대기 : 특정 프로세스가 영원히 임계 영역에 들어가지 못하면 안 된다.
- 융통성 : 한 프로세스가 다른 프로세스의 일을 방해해서는 안 된다.

이 방법에 토대가 되는 메커니즘 - 잠금(lock)
- 예를 들어 임계 영역을 화장실이라고 하면, 화장실에 사람a가 들어간 다음 문을 잠근다. 그리고 다음 사람이 이를 기다리다가 a가 나오면 화장실을 쓰는 방법

**3.7.1. 뮤텍스**
> 프로세스나 스레드가 공유 자원을 lock()을 통해 잠금 설정하고 사용한 후에는 unlock()을 통해 잠금 해제하는 객체

잠금이 설정되면 다른 프로세스나 스레드는 잠긴 코드 영역에 접근할 수 없고 해제는 그 반대이다.
잠금 또는 잠금 해제 상태만을 가진다.
- 구현의 유사성으로 인해 뮤텍스는 바이너리 세마포어라고 할 수 있으나, 잠금을 기반으로 상호 배제가 일어나는 '잠금 매커니즘'이다.


**3.7.2. 세마포어**
> 일반화된 뮤텍스로, 간단한 정수 값과 두 가지 함수 wait(P 함수) 및 signal(V 함수)로 공유 자원에 대한 접근 처리

- wait() : 자신의 차례가 올 때까지 기다리는 함수
	- 프로세스나 스레드가 공유 자원에 접근 시, 세마포어에서 wait() 작업 수행
- signal() : 다음 프로세스로 순서를 넘겨주는 함수
	- 프로세스나 스레드가 공유 자원을 해제 시, signal() 작업 수행

- 조건 변수가 없다.
- 프로세스나 스레드가 세마포어 값을 수정할 때 다른 프로세스나 스레드는 동시에 세마포어 값 수정 불가능

- 바이너리 세마포어
	- 0과 1의 두 가지 값만 가질 수 있는 세마포어
	- 신호를 기반으로 상호 배제가 일어나는 '신호 매커니즘'
	- 신호 매커니즘 : 휴대폰에서 노래를 듣다가 친구로부터 전화가 오면 노래가 중지되고 통화 처리 작업에 관한 인터페이스가 등장하는 것 상상
- 카운팅 세마포어
	- 여러 개의 값을 가질 수 있는 세마포어
	- 여러 자원에 대한 접근을 제어하는 데 사용


**3.7.3. 모니터**
> 둘 이상의 스레드나 프로세스가 공유 자원에 안전하게 접근할 수 있도록 공유 자원을 숨기고 해당 접근에 대해 인터페이스만 제공한다.

모니터큐를 통해 공유 자원에 대한 작업들을 순차적으로 처리한다.
세마포어보다 구현하기 쉬우며 모니터에서 상호 배제는 자동인 반면에, 세마포어에서는 상호 배제를 명시적으로 구현해야 하는 차이점이 있다.



### 3.8. 교착 상태(deadlock)
---
두 개 이상의 프로세스들이 서로가 가진 자원을 기다리며 중단된 상태
- 예
	- 프로세스 a가 프로세스 b의 어떤 자원을 요청할 때 프로세스 b도 프로세스 a가 점유하고 있는 자원을 요청하는 것이다.

**교착 상태 원인**
- 상호 배제 : 한 프로세스가 자원을 독점하고 있으며 다른 프로세스들은 접근이 불가능하다.
- 점유 대기 : 특정 프로세스가 점유한 자원을 다른 프로세스가 요청하는 상태
- 비선점 : 다른 프로세스의 자원을 강제적으로 가져올 수 없다.
- 환형 대기 : 프로세스 a는 프로세스 b의 자원을 요구하고, 프로세스 b는 프로세스 a의 자원을 요구하는 등 서로가 서로의 자원을 요구하는 상황

**교착 상태 해결 방법**
1. 자원을 할당할 때 애초에 조건이 성립되지 않도록 설계한다.
2. 교착 상태 가능성이 없을 때만 자원 할당된다. 프로세스당 요청할 자원들의 최대치를 통해 자원 할당 가능 여부를 파악하는 '은행원 알고리즘' 사용
	- 은행원 알고리즘 : 총 자원의 양과 현재 할당한 자원의 양을 기준으로 안정 또는 불안정 상태로 나누고 안정 상태로 가도록 자원을 할당하는 알고리즘
3. 교착 상태가 발생하면 사이클이 있는지 찾아보고 이에 관련된 프로세스를 한 개씩 지운다.
4. 교착 상태는 매우 드물게 일어나기 때문에 이를 처리하는 비용이 더 커서 교착 상태가 발생하면, 사용자가 작업을 종료한다.
	- 예를 들어 프로세스를 실행시키다 '응답 없음'이 뜰 때 : 교착 상태가 발생한 경우에 이와 같은 경우가 발생한다.



## 4. CPU 스케줄링 알고리즘
---
CPU 스케줄러 : CPU 스케줄링 알고리즘에 따라 프로세스에서 해야 하는 일을 스레드 단위로 CPU에 할당한다.

**CPU 스케줄링 알고리즘**
- 비선점형
	- FCFS
	- SJF
	- 우선순위
- 선점형
	- 라운드로빈
	- SRF
	- 다단계 큐
- 프로그램이 실행될 때 어떤 프로그램에 CPU 소유권을 줄 것인지 결정
- CPU 이용률은 높게, 주어진 시간에 많은 일을 하게 하는 것을 목표로 한다.
- 준비 큐(ready queue)에 있는 프로세스는 적게, 응답 시간은 짧게 설정하는 것을 목표로 한다.


### 4.1. 비선점형 방식
---
> 비선점형 방식 (non-preemptive) : 프로세스가 스스로 CPU 소유권을 포기하는 방식
> 강제로 프로세스를 중지하지 않는다.
> 컨텍스트 스위칭으로 인한 부하가 적다.

**FCFS(First Come, First Served)**
> 가장 먼저 온 것을 가장 먼저 처리하는 알고리즘
- 단점 : 길게 수행되는 프로세스 때문에 '준비 큐에서 오래기다리는 현상(convoy effect)' 발생

**SJF(Shortest Job First)**
> 실행 시간이 가장 짧은 프로세스를 가장 먼저 실행하는 알고리즘
- 긴 시간을 가진 프로세스가 실행되지 않는 현상(starvation)이 일어난다.
- 평균 대기 시간이 가장 짧다.
- 실제로는 실행 시간을 알 수 없기 때문에 과거의 실행했던 시간을 토대로 추측해서 사용한다.

**우선순위**
기존 SJF 스케줄링의 경우 긴 시간을 가진 프로세스가 실행되지 않는 현상이 있었다. 이는 오래된 작업일수록 '우선순위를 높이는 방법(aging)'을 통해 단점을 보완한 알고리즘이다.



### 4.2. 선점형 방식
---
> 선점형 방식 (preemptive) : 현대 운영체제가 쓰는 방식으로, 지금 사용하고 있는 프로세스를 알고리즘에 의해 중단시켜 버리고 강제로 다른 프로세스에 CPU 소유권을 할당하는 방식


**라운드 로빈 (RR, Round Robin)**
> 각 프로세스는 동일한 할당 시간을 주고 그 시간 안에 끝나지 않으면 다시 준비 큐의 뒤로 가는 알고리즘

- 현대 컴퓨터가 쓰는 스케줄링인 '우선순위 스케줄링(priority scheduling)'의 일종
- q만큼의 할당 시간이 부여되었고 N개의 프로세스가 운영된다고 할 때, (N-1) * q 시간이 지나면 자기 차례가 오게 된다. 할당 시간이 너무 크면 FCFS가 되고 짧으면 컨텍스트 스위칭이 잦아져서 오버헤드, 즉 비용이 커진다.
- 일반적으로 전체 작업 시간은 길어지지만 평균 응답 시간은 짧아진다.
- 로드밸런서에서 트래픽 분산 알고리즘으로도 쓰인다.


**SRF (Shortest Remaining Time First)**
>중간에 더 짧은 작업이 들어오면 수행하던 프로세스를 중지하고 해당 프로세스를 수행하는 알고리즘

- SJF와 차이점
	- SJF는 중간에 실행 시간이 더 짧은 작업이 들어와도 기존 짧은 작업을 모두 수행하고 그 다음 짧은 작업을 이어나간다. 


**다단계 큐**
> 우선순위에 따른 준비 큐를 여러 개 사용하고, 큐마다 라운드 로빈이나 FCFS 등 다른 스케줄링 알고리즘을 적용한 것

- 큐 간의 프로세스 이동이 안 되므로 스케줄링 부담이 적다.
- 단점 : 유연성이 떨어진다.

- 높은 우선순위 - 시스템 프로세스 - FCFS -> CPU
- 중간 우선순위 - 상호 작용적인 프로세스 - SJF -> CPU
- 낮은 우선순위 - 배치 프로세스 - RR -> CPU

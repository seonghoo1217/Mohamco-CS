# 2. 컴퓨터의 요소
컴퓨터는 CPU, DMA 컨트롤러, 메모리, 타이머, 디바이스 컨트롤러 등으로 이루어져 있다.

## 2.1. CPU
CPU(Central Processing Unit)는 산술논리연산장치, 제어장치, 레지스터로 구성되어 있는 컴퓨터 장치를 말하며, 인터럽트에 의해 단순히 메모리에 존재하는 명령어를 해석해서 실행하는 일꾼이다.

### 2.1.1. 제어장치
제어장치(CU, Control Unit)는 프로세스 조작을 지시하는 CPU의 한 부품이다. 입출력장치 간 통신을 제어하고 명령어들을 읽고 해석하며 데이터 처리를 위한 순서를 결정한다.

### 2.1.2. 레지스터
레지스터는 CPU 안에 있는 매우 빠른 임시기억장치를 기리킨다. CPU와 직접 연결되어 있으므로 연산 속도가 메모리보다 수십 배에서 수백 배까지 빠르다. CPU는 자체적으로 데이터를 저장할 방법이 없기 때문에 레지스터를 거쳐 데이터를 전달한다.

### 2.1.3. 산술논리연산장치
산술논리연산장치(ALU, Arithmetic Logic Unit)는 덧셈, 뺄셈 같은 두 숫자의 산술 연산과 배타적 논리합, 논리곱 같은 논리 연산을 계산하는 디지털 회로이다.

**CPU의 연산 처리**
CPU에서 제어장치, 레지스터, 산술논리연산장치를 통해 연산하는 예는 다음과 같다.

1. 제어장치가 메모리에 계산할 값을 로드한다. 또한, 레지스터에도 로드한다.
2. 제어장치가 레지스터에 있는 값을 계산하라고 산술논리연산장치에 명령한다.
3. 제어장치가 계산된 값을 다시 '레지스터에서 메모리로' 계산한 값을 저장한다.

### 2.1.4 인터럽트
인터럽트는 어떤 신호가 들어왔을 때 CPU를 잠깐 정지시키는 것을 말한다. 키보드, 마우스 등 IO 디바이스로 인한 인터럽트, 0으로 숫자를 나누는 산술 연산에서의 인터럽트, 프로세스 오류 등으로 발생한다.

인터럽트가 발생되면 인터럽트 핸들러 함수가 모여 있는 인터럽트 벡터로 가서 인터럽트 핸들러 함수가 실행된다. 인터럽트 간에는 우선순위가 있고 우선순위에 따라 실행되며 인터럽트는 하드웨어 인터럽트, 소프트웨어 인터럽트 두 가지로 나뉜다.

>- **인터럽트 핸들러 함수**
   인터럽트가 발생했을 때 이를 핸들리하기 위한 함수, 커널 내부의 IRQ를 통해 호출되며 request_irq()를 통해 인터럽트 핸들러 함수를 등록할 수 있다.

**하드웨어 인터럽트**
하드웨어 인터럽트는 키보드를 연결한다거나 마우스를 연결하는 일 등의 IO 디바이스에서 발생하는 인터럽트를 말한다.

이때 인터럽트 라인이 설계된 이후 순차적인 인터럽트 실행을 중지하고 운영체제에 시스템콜을 요청해서 원하는 디바이스로 향해 디바이스에 있는 작은 로컬 버퍼에 접근하여 일을 수행한다.

**소프트웨어 인터럽트**
소프트웨어 인터럽트는 트랩(trap)이라고도 한다. 프로세스 오류 등으로 프로세스가 시스템콜을 호출할 때 발동한다.

## 2.2. DMA 컨트롤러
DMA 컨트롤러는 I/O 디바이스가 메모리에 직접 접근할 수 있도록 하는 하드웨어 장치를 뜻한다. CPU에만 너무 많은 인터럽트 요청이 들어오기 때문에 CPU 부하를 막아주며 CPU의 일을 부담하는 보조 일꾼이라고 보면 된다. 또한 하나의 작업을 CPU와 DMA 컨트롤러가 동시하는 것을 방지한다.

## 2.3. 메모리
메모리(memory)는 전자회로에서 데이터나 상태, 명령어 등을 기록하는 장치를 말하며, 보통 RAM(Random Access Memory)을 일컬어 메모리라고 한다. CPU는 계산을 담당하고, 메모리는 기억을 담당한다.

공장에 비유하자면 CPU는 일꾼이고, 메모리는 작업장이며, 작업장의 크기가 곧 메모리의 크기이다. 작업장이 클수록 창고에서 물건을 많이 가져다놓고 많은 일을 할 수 있듯이 메모리가 크면 클수록 많은 일을 동시에 할 수 있다.

## 2.4. 타이머
타이머(timer)는 몇 초 안에는 작업이 끝나야 한다는 것을 정하고 특정 프로그램에 시간 제한을 다는 역할을 한다. 시간이 많이 걸리는 프로그램이 작동할 때 제한을 걸기 위해 존재한다.

## 2.5. 디바이스 컨트롤러
디바이스 컨트롤러(device controller)는 컴퓨터와 연결되어 있는 IO 디바이스들의 작은 CPU를 말한다.


프로세스(process)는 컴퓨터에서 실행되고 있는 프로그램을 말하며 CPU 스케줄링의 대상이 되는 작업(task)이라는 용어와 거의 같은 의미로 쓰인다. 스레드는 프로세스 내 작업의 흐름을 지칭한다.

프로그램이 메모리에 올라가면 프로세스가 되는 인스턴스화가 일어나고, 이후 운영체제의 CPU 스케줄러에 따라 CPU가 프로세스를 실행한다.

프로세스와 스레드

# 1. 프로세스와 컴파일 과정
프로세스는 프로그램으로부터 인스턴스화된 것을 말한다.

프로그램은 컴파일러가 컴파일 과정을 거쳐 컴퓨터가 이해할 수 있는 기계어로 번역되어 실행할 수 있는 파일이 되는 것을 의미하며 '컴파일 과정'이란 다음과 같다. 참고로 여기서 말하는 프로그램이란 C 언어 기반의 프로그램을 의미하며, 이는 별도의 컴파일 과정 없이 한 번에 한 줄씩 읽어들여서 실행하는 인터프리터 언어(파이썬 등)으로 된 프로그램과는 다르다.
![](https://velog.velcdn.com/images/cnj9912/post/09906366-e81d-4036-9ad3-1969c8d58980/image.png)

## 1.1. 전처리
소스 코드의 주석을 제거하고 #include 등 헤더 파일을 평합하여 매크로를 치환한다.

## 1.2. 컴파일러
오류 처리, 코드 최적화 작업을 하며 어셈블리어로 변환한다.

## 1.3. 어셈블러
어셈블리어는 목적 코드(object code)로 변환된다. 이때 확장자는 운영체제마다 다른데 리눅스에서는 .o이다.

## 1.4. 링커
프로그램 내에 있는 라이브러리 함수 또는 다른 파일들과 목적 코드를 결합하여 실행 파일을 만든다. 실행 파일의 확장자는 .exe 또는 .out이라는 확장자를 갖는다.

**정적 라이브러리와 동적 라이브러리**
정적 라이브러리는 프로그램 빌드 시 라이브러리가 제공하는 모든 코드를 실행 파일에 넣는 방식이며, 시스템 환경 등 외부 의존도가 낮고 코드 중복 등 메모리 효율성이 떨어지는 단점이 있다.

동적 라이브러리는 프로그램 실행 시 필요할 때만 DLL이라는 함수 정보를 통해 참조하는 방식이며, 메모리 효율성에서의 장점과 외부 의존도가 높아진다는 단점이 있다.

# 2. 프로세스의 상태
## 2.1. 생성 상태
생성 상태(create)는 프로세스가 생성된 상태를 의미하며 fork() 또는 exec() 함수를 통해 생성한다. 이때 PCB가 할당된다.

**fork()**
fork()는 부모 프로세스의 주소 공간을 그대로 복사하며, 새로운 자식 프로세스를 생성하는 함수이다. 주소 공간만 복사할 뿐이지 부모 프로세스의 비동기 작업 등을 상속하지는 않는다.

**exec()**
exec()은 새롭게 프로세스를 생성하는 함수이다.

## 2.2. 대기 상태
대기 상태(ready)는 메모리 공간이 충분하면 메모리를 할당받고 아니면 아닌 상태로 대기하고 있으며 CPU 스케줄러로부터 CPU 소유권이 넘어오기를 기다리는 상태이다.

## 2.3. 대기 중단 상태
대기 중단 상태(ready suspended)는 메모리 부족으로 일시 중단된 상태이다.

## 2.4. 실행 상태
실행 상태(running)는 CPU 소유권과 메모리를 할당 받고 인스트럭션을 수행 중인 상태를 의미한다. 이를 CPU burst가 일어났다고 표현한다.

## 2.5. 중단 상태
중단 상태(blocked)는 어떤 이벤트가 발생한 이후 기다리며 프로세스가 차단된 상태이다. I/O 디바이스에 의한 인터럽트로 이런 현상이 많이 발생한다.

## 2.6. 일시 중단 상태
일시 중단 상태(blocked suspended)는 대기 중단과 유사하다. 중단된 상태에서 프로세스가 실행되려고 했지만 메모리 부족으로 일시 중단된 상태이다.

## 2.7. 종료 상태
종료 상태(terminated)는 메모리와 CPU 소유권을 모두 놓고 가는 상태를 말한다. 종료는 자연스럽게 종료되는 것도 있지만 부모 프로세스가 자식 프로세스를 강제시키는 비자발적 종료(abort)로 종료되는 것도 있다. 자식 프로세스에 할당된 자원의 한계치를 넘어서거나 부모 프로세스가 종료되거나 사용자가 process, kill 등 여러 명령어로 프로세스를 종료할 때 발생한다.

# 3. 프로세스의 메모리 구조

![](https://velog.velcdn.com/images/cnj9912/post/4221ad83-fdbe-4067-bf44-7dc562446072/image.png)

## 3.1. 스택
스택에는 지역변수, 매개변수, 함수가 저장되고 컴파일 시에 크기가 결정되며 '동적'인 특징을 갖는다.

스택 영역은 함수가 함수를 재귀적으로 호출하면서 동적으로 크기가 늘어날 수 있는데, 이때 힙과 스택의 메모리 영역이 겹치면 안 되기 때문에 힙과 스택 사이의 공간을 비워 놓는다.

## 3.2. 힙
힙은 동적 할당할 때 사용되며 런타임 시 크기가 결졍된다. 예를 들어 벡터 같은 동적 배열을 당연히 힙에 동적 할당된다. 힙은 '동적'인 특징을 가진다.

## 3.3. 데이터 영역
데이터 영역은 전역변수, 정적변수가 저장되고, 정적인 특징을 갖는 프로그램이 종료되면 사라지는 변수가 들어 있는 영역이다.

데이터 영역은 BSS 영역과 Data 영역으로 나뉘고, BSS 영역은 초기화 되지 않은 변수가 0으로 초기화되어 저장되며 Data 영역(Data segment)은 0이 아닌 다른 값으로 할당된 변수들이 저장된다.

## 3.4. 코드 영역
코드 영역은 프로그램에 내장되어 있는 소스 코드가 들어가는 영역이다. 이 영역은 수정 불가능한 기계어로 저장되어 있으며 정적인 특징을 가진다.

# 4. PCB
PCB(Process Control Block)는 운영체제에서 프로세스에 대한 메타데이터를 저장한 '데이터'를 말한다. 프로세스 제어 블록이라고도 한다. 프로세스가 생성되면 운영체제는 해당 PCB를 생성한다.

프로그램이 실행되면 프로세스가 생성되고 프로세스 주소 값들에 앞서 설명한 스택, 힙 등의 구조를 기반으로 메모리가 할당된다. 그리고 이 프로세스의 메타데이터들이 PCB에 저장되어 관리된다. 이는 프로세스의 중요한 정보를 포함하고 있기 때문에 일반 사용자가 접근하지 못하도록 커널 스택의 가장 앞부분에서 관리된다.

> - 메타데이터
    데이터에 관한 구조화된 데이터이자 데이터를 설명하는 작은 데이터, 대량의 정보 가운데에서 찾고 있는 정보를 효율적으로 찾아내서 이용하기 위한 일정한 규칙에 따라 콘텐츠에 대해 부여되는 데이터

## 4.1. PCB의 구조
- 프로세스 스케줄링 상태 : '준비', '일시중단' 등 프로세스가 CPU에 대한 소유권을 얻은 이후의 상태
- 프로세스 ID : 프로세스 ID, 해당 프로세스의 자식 프로세스 ID
- 프로세스 권한 컴퓨터 자원 또는 I/O 디바이스에 대한 권한 정보
- 프로그램 카운터 : 프로세스에서 실행해야 할 다음 명령의 주소에 대한 포인터
- CPU 레지스터 : 프로세스를 실행하기 위해 저장해야 할 레지스터에 대한 정보
- CPU 스케줄링 정보 : CPU 스케줄러에 의해 중단된 시간 등에 대한 정보
- 계정 정보 : 프로세스 실행에 사용된 CPU 사용량, 실행한 유저의 정보
- I/O 상태 정보 : 프로세스에 할당된 I/O 디바이스 목록

## 4.2. 컨텍스트 스위칭
컨텍스트 스위칭(context switching)은 앞서 설명한 PCB를 교환하는 과정을 말한다. 한 프로세스에 할당된 시간이 끝나거나 인터럽트에 의해 발생한다. 컴퓨터는 많은 프로그램을 동시에 실행하는 것처럼 보이지만 어떠한 시점에서 실행되고 있는 프로세스는 단 한 개이며, 많은 프로세스가 동시에 구동되는 것처럼 보이는 것은 다른 프로세스와의 컨텍스트 스위칭이 아주 빠르 속도로 실행되기 때문이다.

# 5. 멀티프로세싱
멀티프로세싱은 여러 개의 '프로세스', 즉 멀티프로세스를 통해 동시에 두 가지 이상의 일을 수행할 수 있는 것을 말한다. 이를 통해 하나 이상의 일을 병렬로 처리할 수 있으며 특정 프로세스의 메모리, 프로세스 중 일부에 문제가 발생되더라도 다른 프로세스를 이용해서 처리할 수 있으므로 신뢰성이 높은 강점이 있다.

## 5.1. 웹 브라우저
- 브라우저 프로세스 : 주소 표시줄, 북마크 막대, 뒤로 가기 버튼, 앞으로 가기 버튼 등을 담당하며 네트워크 요청이나 파일 접근 같은 권한을 담당한다.
- 렌더러 프로세스 : 웹 사이트가 '보이는' 부분의 모든 것을 제어한다.
- 플러그인 프로세스 : 웹 사이트에서 사용하는 플러그인을 제어한다.
- GPU 프로세스 : GPU를 이용해서 화면을 그리는 부분을 제어한다.

## 5.2. IPC
멀티프로세스는 IPC(Inter Process Communication)가 가능하며 IPC는 프로세스끼리 데이터를 주고받고 공유 데이터를 관리하는 메커니즘을 뜻한다.

### 5.2.1. 공유 메모리
공유 메모리(shared memory)는 여러 프로세스에 동일한 메모리 블록에 대한 접근 권한이 부여되어 프로세스가 서로 통신할 수 있도록 공유 버퍼를 생성하는 것을 말한다.

기본적으로는 각 프로세스의 메모리를 다른 프로세스가 접근할 수 없지만 공유 메모리를 통해 여러 프로세스가 하나의 메모리를 공유할 수 있따.

### 5.2.2. 파일
파일은 디스크에 저장된 데이터 또는 파일 서버에서 제공한 데이터를 말한다. 이를 기반으로 프로세스 간 통신을 한다.

### 5.2.3. 소켓
동일한 컴퓨터의 다른 프로세스나 네트워크의 다른 컴퓨터로 네트워크 인터페이스를 통해 전송하는 데이터를 의미하며 TCP와 UDP가 있다.

### 5.3.4. 익명 파이프
익명 파이프(unamed pipe)는 프로세스 간에 FIFO 방식으로 읽히는 임시 공간인 파이프를 기반으로 데이터를 주고받으며, 단방향 방식의 읽기 전용, 쓰기 전용 파이프를 만들어서 작동하는 방식을 말한다.

### 5.3.5. 명명된 파이프
명명된 파이프(named pipe)는 파이프 서버와 하나 이상의 파이프 클라이언트 간의 통신을 위한 명명된 단방향 또는 이중 파이프를 말한다. 클라이언트/서버 통신을 위한 별도의 파이프를 제공하며, 여러 파이프를 동시에 사용할 수 있다. 컴퓨터의 프로세스끼리 또는 다른 네트워크상의 컴퓨터와도 통신을 할 수 있다.

### 5.3.6. 메시지 큐
메시지 큐는 메시지를 큐(queue) 데이터 구조 형태로 관리하는 것을 의미한다. 공유 메모리를 통해 IPC를 구형할 때 쓰기 및 읽기 빈도가 높으면 동기화 때문에 기능을 구현하는 것이 매우 복잡해지는데, 이때 대안으로 메시지 큐를 사용하기도 한다.

# 6. 스레드와 멀티스레딩
## 6.1. 스레드
스레드는 프로세스의 실행 가능한 가장 작은 단위이다. 프로세스는 여러 스레드를 가질 수 있다.

코드, 데이터, 스택, 힙을 각각 생성하는 프로세스와는 달리 스레드는 코드, 데이터, 힙은 스레드끼리 서로 공유한다. 그 외의 영역은 각각 생성된다.

## 6.2. 멀티스레딩
멀티스레딩은 프로세스 내 작업을 여러 개의 스레드, 멀티스레드로 처리하는 기법이며 스레드끼리 서로 자원을 공유하기 때문에 효율성이 높다.

동시성에 큰 장정미 있다. 하지만 한 스레드에 문제가 생기면 다른 스레드에도 영향을 끼쳐 스레드로 이루어져 있는 프로세스에 영향을 줄 수 있는 단점이 있다.

> - **동시성**
    서로 독립적인 작업들을 작은 단위로 나누고 동시에 실행되는 것처럼 보여주는 것

# 7. 공유 자원과 임계 영역
## 7.1. 공유 자원
공유 자원(shared resource)은 시스템 안에서 각 프로세스, 스레드가 함께 접근할 수 있는 모니터, 프린터, 메모리, 파일, 데이터 등의 자원이나 변수 등을 의미한다. 이 공유 자원을 두 개 이상의 프로세스가 동시에 읽거나 쓰는 상황을 경쟁 상태(race condition)라고 한다.

## 7.2. 임계 영역
임계 영역(critical section)은 둘 이상의 프로세스, 스레드가 공유 자원에 접근할 때 순서 등의 이유로 결과가 달라지는 코드 영역을 말한다. 임계 영역을 해결하기 위한 방법은 크게 뮤텍스, 세마포어, 모니터 세 가지가 있으며, 이 방법 모두 상호 배제, 한정 대기, 융통성이란 조건을 만족한다. 이 방법에 토대가 되는 메커니즘은 잠금(lock)이다.
> - **상호 배제**
    한 프로세스가 임계 영역에 들어갔을 때 다른 프로세스는 들어갈 수 없다.
- **한정 대기**
  특정 프로세스가 영원히 임계 영역에 들어가지 못하면 안 된다.
- **융통성**
  한 프로세스가 다른 프로세스의 일을 방해해서는 안 된다.

### 7.2.1. 뮤텍스
뮤텍스(mutex)는 프로세스나 스레드가 공유 자원을 lock()을 통해 잠금 설정하고 사용한 후에는 unlock()을 통해 잠금 해재하는 객체이다.

### 7.2.2. 세마포어
세마포어(semaphore)는 일반화된 뮤텍스이다. 간단한 정수 값과 두 가지 함수 wait(P 함수라고도 함) 및 signal(V 함수라고도 함)로 공유 자원에 대한 접근을 처리한다.

wait()는 자신의 차례가 올 때까지 기다리는 함수이며, signal()은 다음 프로세스로 순서를 넘겨주는 함수이다.

### 7.2.3. 모니터
모니터는 둘 이상의 스레드나 프로세스가 공유 자원에 안전하게 접근할 수 있도록 공유 자원을 숨기고 해당 접근에 대해 인터페이스만 제공한다.

모니터는 세마포어보다 구현하기 쉬우면 모니터에서 상호 배제는 자동이 반면에, 세마포어에서는 상호 배제를 명시적으로 구현해야 하는 차이점이 있다.

# 8. 교착 상태
교착 상태(deadlock)는 두 개 이상의 프로세스들이 서로가 가진 자원을 기다리며 중단된 상태를 말한다.

예를 들어 프로세스 A가 프로세스 B의 어떤 자원을 요청할 때 프로세스 B도 프로세스 A가 점유하고 있는 자원을 요청하는 것이다.

## 8.1. 교착 상태의 원인
- 상호 배제 : 한 프로세스가 자원을 독점하고 있으며 다른 프로세스들은 접근이 불가능하다.
- 점유 대기 : 특정 프로세스가 점유한 자원을 다른 프로세스가 요청하는 상태이다.
- 비선점 : 다른 프로세스의 자원을 강제적으로 가져올 수 없다.
- 환형 대기 : 프로세스 A가 프로세스 B의 자원을 요구하고, 프로세스 B도 프로세스 A의 자원을 요구하는 등 서로가 서로의 자원을 요구하는 상황을 말한다.

## 8.2. 교착 상태의 해결 방법
1. 자원을 할당할 때 애초에 조건이 성립되지 않도록 성립한다.
2. 교착 생태 가능성이 없을 때만 자원 할당되며, 프로세스당 요청할 자원들의 최대치를 통해 자운 할당 가능 여부를 파악하는 '은행원 알고리즘'을 쓴다.
3. 교착 상태가 발생하면 사이클이 있는지 찾아보고 이에 관련된 프로세스를 한 개씩 지운다.
4. 교착 상태는 매우 드물게 일어나기 때문에 이를 처리하는 비용이 더 커서 교착 상태가 발생하면 사용자가 작업을 종료한다.

> - 은행원 알고리즘
    총 자원의 양과 현재 할당한 자원의 양을 기준으로 안전 또는 불안정 상태로 나누고 안정 상태로 가도록 자원을 할당하는 알고리즘

CPU 스케줄러는 CPU 스케줄링 알고리즘에 따라 프로세스에서 해야 하는 일을 스레드 단위로 CPU에 할당한다.

프로그램에 실행될 때는 CPU 스케줄링 알고리즘 어떤 프로그램에 CPU 소유권을 줄 것인지 결정한다. 이 알고리즘은 CPU 이용률은 높게, 주어진 시간에 많은 일을 하게, 준비 큐(ready queue)에 있는 프로세스는 적게, 응답 시간은 짧게 설정하는 것을 목표로 한다.

# 1. 비선점형 방식
비선점형 방식(non-preemptive)은 프로세스가 스스로 CPU 소유권을 소유권을 포기하는 방식이며, 강제로 프로세스를 중지하지 않는다. 따라서 컨텍스트 스위칭으로 인한 부하가 적다.

## 1.2. FCFS
FCFS(First Come, First Served)는 가장 먼저 온 것을 가장 먼저 처리하는 알고리즘이다. 길게 수행되는 프로세스 때문에 '준비 큐에서 오래 기다리는 현상(convoy effect)'이 발생하는 단점이 있다.

## 1.3. SJF
SJF(Shortest Job First)는 실행 시간이 가장 짧은 프로세스를 가장 먼저 실행하는 알고리즘이다.

긴 시간을 가진 프로세스가 실행되지 않는 현상(starvation)이 일어나며 평균 대기 시간이 가장 짧다. 하지마 실제로 실행 시간을 알 수 없기 때문에 과거의 실행했던 시간을 토대로 추측해서 사용한다.

## 1.4. 우선순위
기존 SJF 스케줄링의 경우 긴 시간을 가진 프로세스가 실행되지 않는 현상이 있었다.

이는 오래된 작업일수록 '우선순위를 높이는 방법(aging)'을 통해 단점을 보완한 알고리즘을 말한다.

# 2. 선점형 방식
선점형 방식(preemptive)은 형대 운영체제가 쓰는 방식으로 지금 사용하고 있는 프로세스를 알고리즘에 의해 중단시켜 버리고 강제로 다른 프로세스에 CPU 소유권을 할당하는 방식을 말한다.

## 2.1. 라운드 로빈
라운드 로빈(RR, Round Robin)은 현대 컴퓨터가 쓰는 스케줄링인 우선순위 스케줄링(priority scheduling)의 일종으로 각 프로세스는 동일한 시간을 주고 그 시간 안에 끝나지 않으면 다시 준비 큐(ready queue)의 뒤로 가는 알고리즘이다.

## 2.2. SRF
SJF는 중간에 실행 시간이 더 짧은 작업이 들어와도 기존 짧은 작업을 모두 수행하고 그다음 짧은 작업을 이어나가는데, SRF는 중간에 더 짧은 작업이 들어오면 수행하던 프로세스를 중지하고 해당 프로세스를 수행하는 알고리즘이다.

## 2.3. 다단계 큐
다단계 큐는 우선순위에 따른 준비 큐를 여러 개 사용하고, 큐마다 라운드 로빈이나 FCFS 등 다른 스케줄링 알고리즘을 적용한 것을 말한다. 큐 간의 프로세스 이동이 안되므로 스케줄링 부담이 적지만 유연성이 떨어지는 특징이 있다.
# IP 주소

### ARP

컴퓨터와 컴퓨터가 통신할 때 IP 주소를 기반으로 하는데, 정확히 IP 주소의 ARP를 통해 MAC 주소를 찾아 MAC 주소를 기반으로 통신한다.

ARP(Address Resolution Protocol)란 IP주소로부터 MAC 주소를 구하는 IP와 MAC 주소의 다리 역할을 하는 프로토콜이다.

ARP를 통해 가상 주소인 IP 주소를 실제 주소인 MAC 주소로 변환한다.

RARP를 통해 실제 주소인 MAC 주소를 가상 주소인 IP 주소로 변환한다.

논리적 주소(IP) → ARP → 물리적 주소(MAC)

물리적 주소(MAC) → RARP → 논리적 주소(IP)

**주소를 찾는 과정 (ARP)**

장치 A가 ARP Request 브로드캐스트를 보내서 IP 주소인 120.70.80.3에 해당하는 MAC 주소를 찾는다.

해당 주소에 맞는 장치 B가 ARP reply 유니캐스트를 통해 MAC 주소를 변환하는 과정을 거쳐 IP 주소에 맞는 MAC 주소를 찾게 된다.

브로드캐스트 : 송신 호스트가 전송한 데이터가 네트워크에 연결된 모든 호스트에게 전달된 방식

유니캐스트 : 고유 주소로 식별된 하나의 네트워크 목적지에 1:1로 데이터를 전송하는 방식

### 홉바이홉 통신

IP 주소를 통해 통신하는 과정을 홉바이홉 통신이다.

여기서 홉(hop)이란 뜻은 건너뛰는 모습을 의미한다.

통신망에서 각 패킷이 여러 개의 라우터를 건너가는 모습을 비유적으로 표현한 것이다.

패킷은 출발지부터 라우터의 라우팅 과정을 거쳐 목적지까지 도착하게 된다.

라우팅이란 중간의 수많은 네트워크에 있는 라우터의 라우팅 테이블 IP를 기반으로 다음 IP로 패킷이 이동하는 과정을 말한다.

라우팅 과정을 거쳐 최종 목적지까지 도달하는 통신을 홉바이홉 통신이라고 한다.

**라우팅 테이블**

라우팅 테이블은 송신지에서 수신지까지 도달하기 위해 사용되며 라우터에 들어가 있는 목적지 정보들과 그 목적지로 가기 위한 방법이 들어 있는 리스트를 말한다.

라우팅 테이블에는 게이트웨이와 모든 목적지에 대해 해당 목적지에 도달하기 위해 거쳐야 할 다음 라우터의 정보를 가지고 있다.

**게이트웨이**

서로 다른 통신망, 프로토콜을 사용하는 네트워크 간의 통신을 가능하게 하는 관문 역할을 하는 컴퓨터나 소프트웨어를 두루 일컫는 용어이다.

사용자는 인터넷에 접속하기 위해 수많은 게이트웨이를 거쳐야 하며 게이트웨이는 서로 다른 네트워크상의 통신 프로토콜을 변환해주는 역할을 하기도 한다.

`netstat -r` 명령어로 라우팅 테이블을 확인할 수 있다. (게이트웨이, 인터페이스 등)

## IP주소 체계

IP주소는 IPv4와 IPv6로 나뉜다.

IPv4는 32비트를 8비트 단위로 점을 찍어 표기한다. 123.45.67.89

IPv6는 64비트를 16비트 단위로 점을 찍어 표기한다. 2001:db8:ff00:42:8329

### 클래스 기반 할당 방식

IP 주소 체계는 과거를 거쳐 발전해오고 있으며 초기에는 A,B,C,D,E 다섯 개의 클래스로 구분하는 클래스 기반 할당 방식을 썼다.

앞에 있는 부분을 네트워크 주소, 그 뒤에 있는 부분을 컴퓨터에 부여하는 주소인 호스트 주소로 놓아서 사용한다.

A, B, C는 일대일 통신으로 사용하고, D는 멀티캐스트 통신, E는 예비용 주소이다.

A, B, C의 범위는 다음과 같다.

클래스 A : 0.0.0.0 ~ 127.255.255.255

클래스 B : 128.0.0.0 ~ 191.255.255.255

클래스 C : 192.0.0.0 ~ 223.255.255.255

이진수로 표현할 경우 맨 왼쪽에 있는 비트를 구분비트라고 하며, 이를 통해 클래스간 IP가 나뉜다.

A는 0, B는 10, C는 110이다.

네트워크의 첫 번째 주소는 네트워크 주소로 사용디고 가장 마지막 주소는 브로드캐스트용 주소로 사용된다.

**예시**

클래스 A로 12.0.0.0이란 네트워크를 부여받았다.

그렇다면 12.0.0.1 ~ 12.255.255.254의 호스트 주소를 부여받은 것이다.

### DHCP

DHCP(Dynamic Host Configuration Protocol)는 IP 주소 및 기타 통신 매개변수를 자동으로 할당하기 위한 네트워크 관리 프로토콜이다.

이 기술을 통해 네트워크 장치의 IP 주소를 수동으로 설정할 필요 없이 인터넷에 접속할 때마다 자동으로 IP 주소를 할당할 수 있다.

라우터와 게이트웨이 장비 대부분에 DHCP 기능이 있으며 이를 통해 대부분의 가정용 네트워크에서 IP 주소를 할당한다.

### NAT

NAT(Network Address Translation)는 패킷이 라우팅 장치를 통해 전송되는 동안 패킷의 IP 주소 정보를 수정하여 IP 주소를 다른 주소로 매핑하는 방법이다.

IPv4 주소 체계만으로는 많은 주소들을 감당하지 못하기 때문에 NAT로 공인 IP와 사설 IP로 나눠서 많은 주소를 처리한다.

NAT를 가능하게 하는 소프트웨어는 ICS, RRAS, Netfilter 등이 있다.

NAT 장치를 통해 여러 호스트에 주소를 부여하고 하나의 공인 IP로 외부 인터넷에 요청을 할 수 있다.

**공유기와 NAT**

NAT을 주로 쓰는 이유는 주로 여러 대의 호스트가 하나의 공인 IP 주소를 사용하여 인터넷에 접속하기 위함이다.

인터넷 회선 하나를 개통하고 인터넷 공유기를 달면 여러 PC를 연결하여 사용할 수 있다.

→ 인터넷 공유기에 NAT 기능이 탑재되어 있다.

내부 네트워크에서 사용하는 IP 주소와 외부에 드러나는 IP 주소를 다르게 유지할 수 있기 때문에 내부 네트워크에 대한 어느정도 보안이 가능하다.

다만 여러 호스트가 동시에 인터넷에 접속하면 접속 속도가 느려질 수 있다.

# HTTP

HTTP는 전송 계층 위에 있는 애플리케이션 계층에 존재하고 웹 서비스 통신에 사용된다.

HTTP/1.0 부터 HTTP/3 발전되었다.

### HTTP/1.0

HTTP/1.0은 기본적으로 한 연결당 하나의 요청을 처리하도록 설계되었다.

서버로부터 요청을 보내 작업을 할 때 마다 TCP 3-way handshake를 계속해서 해야된다.

→ RTT 증가

RTT : 패킷이 목적지에 도달하고 나서 다시 출발지로 돌아오기까지 걸리는 시간(패킷 왕복 시간)

**RTT의 증가를 해결하기 위해 사용한 방법**

이미지 스플리팅 : 많은 이미지가 합쳐 있는 하나의 이미지를 다운로드 받고, backgroun-image의 position을 이용하여 이미지를 표기하는 방법

코드 압축 : 개행 문자, 빈칸을 없애서 코드의 크기를 최소화

이미지 Base64 인코딩 : 이미지 파일을 64진법으로 이루어진 문자열로 인코딩

### HTTP/1.1

HTTP/1.0처럼 매번 TCP 연결을 하는 것이 아니라 한 번 TCP 초기화를 한 이후에 keep-alive라는 옵션으로 여러 개의 파일을 송수신할 수 있게 되었다.

파일을 전송할 때마다 TCP 3-way handshake를 하지 않아도 된다.

**HOL Blocking**

Head Of Line Blocking은 네트워크에서 같은 큐에 있는 패킷들이 첫 번재 패킷에 의해 지연될 때 발생하는 성능 저하 현상을 말한다.

큐의 맨 앞에 image.png 파일이 다운로드가 느려지게 되면 뒤에 대기하는 파일들의 다운로드가 지연된다.

**무거운 헤더 구조**

HTTP/1.1의 헤더에는 쿠키 등 많은 메타데이터가 들어있고 압축되지 않아 무겁다.

### HTTP/2

HTTP/2는 HTTP/1.x 보다 지연 시간을 줄이고 응답 시간을 더 빠르게 할 수 있으며 멀티플렉싱, 헤더 압축, 서버 푸시, 요청의 우선순위 처리를 지원하는 프로토콜이다.

**멀티플렉싱**

여러 개의 스트림을 사용하여 송수신한다는 것이다.

특정 스트림의 패킷이 손실되었다고 하더라도 해당 스트림에만 영향을 미치고 나머지 스트림은 멀쩡하게 동작할 수 있다.

하나의 연결 내에 여러 스트림을 담아 데이터를 전송할 수 있다.

→ 단일 연결을 사용하여 병렬로 여러 요청을 받을 수 있고 응답을 줄 수 있다.

**헤더 압축**

HTTP/2는 헤더 압축을 사용하는데, 허프만 코딩 압축 알고리즘을 사용하는 HPACK 압축 형식을 가진다.

**서버 푸시**

HTTP/1.1에서는 클라이언트가 서버에 요청을 해야 파일을 다운로드받을 수 있지만, HTTP/2는 클라이언트 요청없이 서버가 바로 리소스를 푸시할 수 있다.

- 서버 푸시 X

html 파일 요청 → html 응답

css 파일 요청 → css 응답

- 서버 푸시

html 파일 요청 → html 응답

→ css 파일 푸시

### HTTPS

HTTP/2는 HTTPS 위에서 동작한다.

HTTPS는 애플리케이션 계층과 전송 계층 사이에 신뢰 계층인 SSL/TLS 계층을 넣은 신뢰할 수 있는 HTTP 요청을 말한다.

이를 통해 통신을 암호화할 수 있다.

**SSL/TLS**

SSL(Secure Socket Layer)은 SSL 1.0부터 2.0, 3.0, TLS(Transport Layer Security Protocol) 1.0, 1.3까지 버전이 있고, TLS로 명칭이 변경되었으나 보통 SSL/TLS로 부른다.

SSL/TLS는 전송 계층에서 보안을 제공하는 프로토콜이다.

클라이언트와 서버가 통신할 때 제3자가 메시지를 도청하거나 변조하지 못하도록 한다.

→ 공격자가 서버인 척하며 사용자 정보를 가로채는 네트워크 상의 인터셉터를 방지할 수 있다.

SSL/TLS는 보안 세션을 기반으로 데이터를 암호화하며 보안 세션이 만들어질 때 인증 메커니즘, 키 교환 암호화 알고리즘, 해싱 알고리즘이 사용된다.

**보안 세션**

보안이 시작되고 끝나는 동안 유지되는 세션을 말한다.

SSL/TLS는 핸드셰이크를 통해 보안 세션을 생성하고 이를 기반으로 상태 정보 등을 공유한다.

**TLS의 핸드셰이크**

클라이언트와 서버가 키를 공유하고 이를 기반으로 인증, 인증 확인 등의 작업이 일어나는 1-RTT가 생긴 후 데이터를 송수신한다.

TLS 1.3은 사용자가 이전에 방문한 사이트로 다시 방문한다면 SSL/TLS에서 보안 세션을 만들 때 걸리는 토잇ㄴ을 하지 않아도 된다. (0-RTT)

클라이언트에서 사이퍼 슈트(cypher suites)를 서버에 전달하면 서버는 받은 사이퍼 슈트의 암호화 알고리즘 리스트를 제공할 수 있는 확인한다.

제공할 수 있다면 서버에서 클라이언트로 인증서를 보내는 인증 메커니즘이 시작되고 이후 해싱 알고리즘 등으로 암호화된 데이터의 송수신이 시작된다.

사이퍼 슈트는 프로토콜, AEAD 사이퍼 모드, 해싱 알고리즘이 나열된 규약이다.

AEAD 사이퍼 모드 : 데이터 암호화 알고리즘이다.

**인증 메커니즘**

CA(Certificate Authorities)에서 발급한 인증서를 기반으로 이루어진다.

CA에서 발급한 인증서는 안전한 연결을 시작하는 데 있어 필요한 공개키를 클라이언트에 제공하고 사용자가 접속한 ‘신뢰할 수 있는’ 서버임을 보장한다.

인증서는 서비스 정보, 공개키, 지문, 디지털 서명 등으로 이루어져 있다.

**암호화 알고리즘**

키 교환 알고리즘은 디피-헬만 방식을 근간으로 만들어졌다.

- 디피-헬만 키 교환 알고리즘

암호키를 교환하는 하나의 방법이다.

각자의 공개 값 공유 → 각자의 비밀 값과 혼합 = 혼합 값

서로에게 혼합 값을 공유 → 각자의 비밀 값과 혼합 = 공통의 암호키 생성

1. 클라이언트와 서버 모두 개인키와 공개키를 생성
2. 서로에게 공개키를 보내고 공개키와 개인키를 결합하여 PSK(사전 합의된 비밀키) 생성

→ 악의적인 공격자가 개인키 또는 공개키를 가지고도 PSK가 없기 때문에 키를 암호화할 수 있다.

### HTTPS 구축 방법

1. 직접 CA에서 구매한 인증키를 기반으로 HTTPS 서비스 구축
2. 서버 앞단에 HTTPS를 제공하는 로드밸런서 두기
3. 서버 앞단에 HTTPS를 제공하는 CDN 두기

### HTTP/3

TCP 위에서 돌아가는 HTTP/2와 달리 QUIC라는 계층 위에서 돌아가며, UDP 기반이다.

QUIC는 TCP를 사용하지 않기 때문에 통신을 시작할 때 3-way handshake 과정을 거치지 않아도 된다.

QUIC는 첫 연결 설정에 1-RTT만 소요된다.

클라이언트가 서버에 어떤 신호를 한 번 주고, 서버도 거기에 응답하기만 하면 본 통신을 바로 시작할 수 있다.

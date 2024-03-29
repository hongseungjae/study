# 운영체제 / 논리회로 일반
### 컴퓨터는 10진수를 2진수로 바꿔서 계산합니다. 10진수를 2진수로 바꾸는 방법과, 그 반대 방법에 대해 설명해 주시기 바랍니다.

* 내 대답 : 10진수에서 일단 2진수로 바꾸는 방법은 예를 들어서 10을 2로 계속 나누고 나머지 값들을 취해서 2진수로 나타낼수 있고, 그 반대는 10진수의 자릿수마다 2의 0승부터 1승 , 2승 이렇게 한 값을 모두 더해서 10진수로 바꿀 수 있습니다.


### 컴퓨터는 소숫점 계산을 잘 못합니다. 그 이유가 무엇일까요? 어떻게 문제를 해결할 수 있을까요? 직접 구현한다면 어떻게 하시겠습니까?

* 내 대답 : 소수점도 마찬가지로 컴퓨터는 2진수로 계산을 합니다. 그런데 소숫점을 이진법으로 계산할 경우 무한소수가 나타날 수 있습니다. 따라서 컴퓨터는 언어에서 부동소숫점을 사용하고 있습니다. 그리고 자바같은 경우는 정확한 소수점 계산을 하기위해서는 보통 빅데시멀이라는 클래스를 사용합니다.

* 정답 : 컴퓨터가 소수점 계산에서 정확도 문제가 발생하는 이유는 소수를 이진수로 변환하면 무한소수가 되어, 컴퓨터에서는 유한한 비트 수로 표현하려고 하기 때문입니다. 이로 인해 정확한 값을 표현하지 못하고 근사값을 사용하게 되며, 이 근사값이 누적되면서 오차가 증가하여 최종 결과에 오차가 발생하는 것입니다.
(소수 부분인 0.14를 2진수로 변환합니다. 0.14을 2로 곱하면 0.28이 됩니다. 여기서 정수 부분인 0은 2진수로 0으로 나타내고)

이러한 문제를 해결하기 위해 컴퓨터에서는 부동 소수점 방식을 사용합니다. 부동 소수점 방식에서는 소수점 위치를 고정하지 않고, 지수와 가수로 구분하여 표현합니다. 이렇게 함으로써 큰 수와 작은 수 모두를 표현할 수 있으며, 정밀도를 조절할 수 있게 됩니다.


또한, 부동 소수점 방식에서도 오차는 발생할 수 있습니다. 이를 해결하기 위해 컴퓨터에서는 반올림 오차 방식을 사용합니다. 이 방식은 계산 결과를 반올림하여 오차를 최소화합니다. 또한, 고정 소수점 방식을 사용하는 경우에는 가능한 한 정밀도를 높이는 것이 중요합니다. 이를 위해 컴퓨터에서는 정밀도를 높이기 위해 라이브러리를 사용하거나, 고정 소수점 방식을 사용하지 않고 부동 소수점 방식을 사용하는 것이 일반적입니다.

최소화폐 찾아보기


### Thread 간의 데이터 공유와 Process 간의 데이터 공유의 공통점과 차이점을 설명해주세요.

* 내 대답 : Thread같은 경우는 힙 영역을 공유하고 있기 때문에 바로 접근 하여 데이터를 가져올수 있습니다. 그러나 프로세스의 경우는 추가적인 일들이 필요합니다. 예를 들어 소켓 연결이나 어떤 프로세스 간의 통신을 위해 통로를 연결하는 작업들이 추가적으로 필요하기때문에 비용이 더 많이 듭니다.

* 정답 : 1. Thread 간의 데이터 공유는 메모리를 공유하기 때문에 공유하는 데이터에 대한 접근이 빠릅니다. 반면, Process 간의 데이터 공유는 프로세스 간의 통신(IPC)을 사용하기 때문에 Thread 간의 데이터 공유보다 느릴 수 있습니다.

2.Thread 간의 데이터 공유는 스레드 간에 데이터를 전달하기 위해 별도의 통신 기능이 필요하지 않습니다. 반면, Process 간의 데이터 공유는 데이터를 전달하기 위해 명시적인 통신 기능(IPC)을 사용해야 합니다.

3. Thread 간의 데이터 공유는 프로세스 내의 스레드들이 동일한 주소 공간에서 실행되기 때문에 동기화 작업이 더 쉽습니다. 반면, Process 간의 데이터 공유는 서로 다른 주소 공간에서 실행되기 때문에 공유 데이터의 일관성과 동기화 작업이 더 어렵습니다


### 컴퓨터가 기계어를 읽고, 실행하는 과정에 대해 설명해 주실 수 있나요?
* 내 대답 : 기계어가 일단 파일이라면 그 파일을 메모리에 올리고 cpu 가져와서 이제 하나씩 해석하는 형태로 작동합니다.

* 정답 : Fetch Execute Cycle 설명
Instruction Fetch Cycle(명령문을 Fetch-Decode-Load-Execute하는 과정)에 따라 그 명령문을 하나씩 실행하게 된다. 
1. 다음에 실행할 명령어를 주기억 장치로 부터 읽어들인다. (Fetch)

2. 명령어를 디코드(해석) 한다. (Decode)

3. 피연산자 Operand를 주기억 장치로 부터 읽어온다. (Operand)

4. 명령어를 실행한다. (Execute)


### 운영체제가 여러 프로그램을 동시에 실행하는 원리에 대해 설명해주세요.
* 내 대답 : 멀티프로세스가 동작하는 원리는 예를 들어 cpu가 1개일 때 프로세스 1번과 2번이 있을 때 두 개를 번갈아 가면서 빠르게 실행하게 됩니다. 이때 사용자는 동시에 작동하는 것처럼 보이게 됩니다. 그리고 cpu가 프로세스 1번을 동작시키다가 인터럽트나, 아니면 버스터 시간이 다 되어있을 때 다시 2번을 동작시키고 이런식으로 동작하게 됩니다.

### 컴파일러와 인터프리터는 어떤 차이가 있을까요?
* 내 대답 : 컴파일러는 한번에 쭉 읽어서 처리하는것이고, 인터프리터는 한줄한줄씩 해석하기 때문에 좀 더 느리다고 볼 수 있습니다.

* 컴파일러는 모든 코드를 미리 기계어로 번역해둔 다음에 실행한다. 하지만 인터프리터는 코드를 한줄한줄 실시간으로 번역하고 실행한다
* 컴파일러는 프로그램의 실행 속도가 빠르다는 장점이 있습니다, 컴파일러는 번역된 기계어 코드가 다른 운영체제에서는 동작하지 않는다는 문제점
* 인터프리터는 운영체제나 하드웨어에 독립적이기 때문에, 한 번 작성한 코드가 여러 운영체제에서 동작할 수 있다는 장점도 있습니다.



### Garbage Collection 이란 무엇일까요? Garbage Collection 방식 중 제일 잘 알고 계시는 GC를 아무거나 하나만 설명해주세요.
* 내 대답 : 가비지 컬렉션은 자바에서 자동으로 메모리를 해제시켜주는 기술 입니다. 그래서 사용자가 일일히 메모리를 쓰고 해제시켜주는 것이 아닌 가비지 컬렉터가 적당한 때에 메모리를 해제시켜줍니다. 가장 잘 알고 있는 gc는 패러렐 gc 입니다. 패러렐 gc는 풀gc가 돌 때 멀티쓰레드로 동작하여 좀 더 빠르게 full gc가 동작할 수 있게 해줍니다.


### Garbage collection 이 있는 언어를 원자력 발전소, 자동차 동력 제어, 인공위성, 국가 전력망 제어시스템 같은 곳에 쓸 수 있을까요? 후보자님의 생각을 말씀해 주세요.
* 내 대답 : 위에 것들은 모두 순간순간에 동작하지 않으면 큰일이 나는 것들입니다. 그런데 가비지 컬렉션은 스탑더월드라고 gc가 돌 때 전체 쓰레드가 멈추게 됩니다. 따라서 이러면 안되기때문에 가비지 컬렉션 언어를 사용하면 안될 것 같습니다.


### 지금 이용하시는 기술/언어에서 제일 마음에 드는점과 불만인 점 한가지를 말씀해주세요.
* 내 대답 : 자바라는 언어를 사용하고 있습니다. 장점으로는 일단 가비지 컬렉션과 객체지향언어 이기때문에 좀 더 친숙하게 짤 수 있습니다. 단점은 c언어에 비하여 속도가 좀 더 느리고, 다른 언어들에 비하여 코드 양이 더많다고 느꼈습니다.

* 추가 답변 : 
운영체제나 하드웨어 등에 관계 없이 실행 가능: 자바는 플랫폼 독립적으로 개발되었기 때문에 운영체제나 하드웨어에 영향을 받지 않고 실행됩니다.
객체 지향 프로그래밍 언어: 자바는 객체 지향적인 프로그래밍 언어로, 코드의 재사용성과 유지보수성이 높아지는 장점이 있습니다.
메모리 관리를 자동으로 처리: 자바는 가비지 컬렉션(Garbage Collection) 기능을 제공하여 개발자가 메모리 관리에 대한 부담과 위험을 줄일 수 있습니다.


### System call 이 뭔가요? System call 에 대해 설명해주세요.
* 내 대답 : 운영체제에서 cpu에게 어떤 명령을 처리하도록 하게 만드는 명령입니다. 예를 들어서 시스템에 쓰기 명령이 들어오면 이것도 system call이고, 인터럽트도 시스템콜의 한 종류 입니다.

* 정답 :  인터럽트는 아님 (인터럽트는 프로그램이 컴퓨터에서 동작하고 있을 때, 입출력 연산 혹은 예외상황이 발생하여 처리가 필요할 때 이를 마이크로 프로세서에게 알려 처리를 할 수 있도록 하는 것을 말합니다.)

* 어떤 프로그램이 컴퓨터의 자원을 사용할수 있게 os에게 부탁하는 것입니다.(커널에 접근할 수 있게) 예를 들어 i/o작업을 하기위해서 이러한 시스템콜을 하게 됩니다.,, 왜 이런 시스템콜이 있냐면 일단 컴퓨터의 자원에 함부로 접근하거나, 다른 프로세스의 자원을 침범하게 안되기 때문 입니다.
* 
사용자 프로그램의 I/O 과정
1. 사용자 프로그램이 운영체제에게 I/O를 요청하는 시스템콜을 한다.
2. Trap(소프트웨어 인터럽트)를 통해 인터럽트 벡터의 위치로 이동한다.
3. 제어권이 인터럽트 벡터가 가리키는 인터럽트 서비스 루틴으로 이동한다.
4. 올바른 I/O 작업인지 확인 후, 실제 I/O를 수행한다.
5. I/O 완료 시 제어권을 시스템콜 다음 명령으로 옮긴다.


### 바이트코드와 기계어의 차이에 대해 설명해주세요.
* 내 대답 : 자바에서는 바이트 코드는 jvm이 해석하기 위한 코드로, 자바를 컴파일하면 바이트 코드가 나오고, 그것을 이제 os가 해석하기 위해 다시 기계어 번역을 합니다.

* 추가 정답 : 이러한 바이트 코드의 장점은 os를 종속적이지 않습니다. 

### Thread safety 란 뭔가요? 어떻게 구현해야 Thread safe 한 코드를 만들 수 있나요?
* 내 대답 : 동시성의 문제라고 생각합니다. 동시에 접근했을 때 값이나 이런것들이 달라지지 않고 일관성 있게 처리할 수 있게 만드는게 쓰레드 세이프티라고 생각하는데, 보통 자바에서 이것을 구현하기 위해서는 싱크로나이즈드를 선언해서 순간에 한쓰레드만 접근할 수 있게 처리를 하거나, 아니면 아예 불변으로 만들어서 처리할 수 있습니다.

* 추가 답변 : 
동기화(synchronization): 동시에 여러 스레드가 접근할 수 있는 자원(공유 변수 등)에 대해서, 해당 자원에 대한 접근을 동기화하여 여러 스레드가 동시에 접근하지 못하도록 막는 방법입니다. 자바에서는 synchronized 키워드를 사용하여 동기화를 구현할 수 있습니다.

불변(Immutable) 객체 사용: 객체의 상태를 변경할 수 없게끔 만들어 스레드 안전성을 보장할 수 있습니다. 불변 객체는 한 번 생성되면 상태를 변경할 수 없으며, 새로운 상태를 가진 객체를 생성하여 반환합니다.

스레드 로컬(Thread-local) 변수 사용: 각 스레드마다 독립적인 변수를 사용하여 공유 변수의 접근을 최소화합니다. 자바에서는 ThreadLocal 클래스를 사용하여 스레드 로컬 변수를 구현할 수 있습니다.

volatile 키워드 사용: 해당 변수를 쓰기나 읽기 전에 항상 메인 메모리에서 읽거나 써야 함을 보장하여 동시에 여러 스레드가 해당 변수를 수정하지 않도록 합니다.

Thread safe한 자료 구조 사용: Vector, ConcurrentHashMap, CopyOnWriteArrayList 등의 자료 구조를 사용하여 여러 스레드가 동시에 접근해도 안전하게 동작합니다.

### bytecode 기반 언어는 디컴파일에 특히 취약하다는 문제가 있는데, 언어를 바꾸지 않고 이를 해결할 방법이 없을까요?
* 내 대답 : 저도 디컴파일을해서 봤을 때 자바 그 코드를 다 보았고, 이것을 해결하기 위해서 뭔가를 추가하여 암호화를 하는 그런 옵션들이 있지 않을까 생각중인데, 잘 모르겠습니다.
* 정답 : 난독화를 할 수 있는 방법이 있습니다. 코드의 의미를 바꾸지 않으면서 코드를 어렵게 만들어 해커나 디컴파일러로부터 코드를 보호하는 기술입니다.
이러한 방식으로 난독화를 수행하면 디버깅이나 코드 분석도 어려워질 수 있으므로, 적절한 수준의 난독화가 필요합니다.


### 파이프(|) 란 무엇이고, 어떻게 동작하는지 설명해주세요.
* 내 대답 : os에 파이프는 앞에 있는 결과값들을 뒤로 넘겨주는 역할을 합니다. 그래서 리눅스같은 경우는 ls를 쳤을때 파일 리스트들이 나오는데 이것들을 파이프라인을 치고 grep을 치면 이 결과값들중에 원하는 키워드를 넣으면 해당 결과만 볼 수 있습니다.
* 추가답변 : 여러 개의 프로세스를 조합하여 한 번에 처리할 수 있도록 하는 기능입니다. 파이프는 쉘(Shell)에서 명령어를 입력할 때 사용되며, 입력한 명령어의 결과를 다른 명령어로 넘겨주는 역할을 합니다


# 네트워크
### Socket 으로 바로 통신하는 것 대비 HTTP 는 비효율적인데도 왜 많은 앱들은 HTTP 를 쓰는 걸까요?
* 내 대답 : 아... HTTP를 통신할 시 html이나 json 이런 형식을 효율적으로 사용할 수 있어서 그런 것 같습니다.
* HTTP는 네트워크 프로토콜 중 하나로, 클라이언트와 서버 간에 데이터를 주고받을 수 있는 방법 중 하나입니다. HTTP는 일반적으로 웹 브라우저와 웹 서버 간의 통신에 사용됩니다.

Socket 프로그래밍을 사용하여 직접 통신하는 것은 빠르고 효율적인 방법이지만, 이는 일반적으로 웹 애플리케이션과 같은 인터넷 기반 애플리케이션에서는 적합하지 않습니다. 이는 네트워크 환경에서 안정성, 보안 등 다양한 이슈를 고려해야하기 때문입니다.

HTTP는 이러한 이슈들을 해결하기 위해 다양한 기능과 보안 메커니즘을 제공합니다. 또한, HTTP는 웹 애플리케이션에서 사용되는 다양한 프레임워크와 라이브러리에서 지원되므로 개발자들이 쉽게 사용할 수 있습니다.

또한, HTTP는 RESTful API를 사용하여 데이터를 전송하고 받을 수 있으며, 이는 다른 시스템과의 상호 운용성을 보장하고, 클라이언트와 서버 간의 상호 작용을 간소화하며, 보안을 향상시킬 수 있습니다.

따라서, HTTP는 일반적으로 네트워크 기반 애플리케이션에서 사용하기에 적합한 방법입니다. 단순한 데이터 전송에 있어서는 Socket을 사용하는 것이 효율적일 수 있지만, 복잡한 애플리케이션을 개발하는 경우에는 HTTP를 사용하는 것이 더욱 안정적이고 유연합니다.

### OSI Layer 7 또는 TCP Model 에 대해 설명해주세요.
물리 계층 (Physical Layer) : 데이터를 전기적인 신호로 변환 주고 받는 기능
데이터 링크 계층 (Data Link Layer) : mac 주소로 변환 해석
네트워크 계층 (Network Layer) : ip로 라우팅을 하여 패킷을 전송
전송 계층 (Transport Layer) : 프로세스 간의 연결을 설정하고, 데이터의 흐름을 제어하며, 오류 검출 및 정정, 흐름 제어, 혼잡 제어 등을 수행합니다. 이 계층에서 사용되는 프로토콜로는 TCP, UDP 등이 있습니다
세션 계층 (Session Layer)
표현 계층 (Presentation Layer)
응용 계층 (Application Layer)
반면에 TCP/IP 모델은 인터넷 프로토콜 스위트의 핵심 프로토콜인 TCP (Transmission Control Protocol)와 IP (Internet Protocol)를 기반으로 한 모델입니다. OSI 7계층과 다르게 TCP/IP 모델은 4개의 계층으로 구성됩니다.

네트워크 액세스 계층 (Network Access Layer)
인터넷 계층 (Internet Layer)
전송 계층 (Transport Layer)
응용 계층 (Application Layer)



### 차세대 프로토콜로 논의중인 HTTP/3 은 UDP 기반의 QUIC 이라는 기술로 구현되어 있습니다. UDP 는 TCP 대비 안정성이 떨어지는 프로토콜이라고 하는데, 그럼에도 왜 UDP 를 채택한 걸까요?
* UDP는 헤더에가 tcp비해 가볍기 때문에 커스텀 마이징에 용이하고, UDP 기반으로 TCP handshake 과정을 없애고 커넥션의 id를 부여하여 사용함
* tcp의 3way handshake의 최적화를 위한 udp


### SSL (또는 TLS) 가 어떻게 동작하는지 말씀해주세요.
* http를 먼저 3way handshake로 연결을 하고 https 는 4way handshake로 연결을 합니다. <- 4way handshake는 종료시네;;

* 클라이언트는 서버에게 지원하는 암호화 알고리즘이나 tls 버전, 난수 값들을 전달하고 서버는 맞는 알고리즘을 선택하고 CA로 부터 발급받은 인증서를 클라이언트에게 전송합니다 
그 다음 클라이언트는 이 인증서를 공개키로 복호화 시키고 그 안의 서버의 공개 키로 임시 대칭키를 만들어서 다시 암호화후 보냅니다.
서버는 다시 복호화 후 이 임시 대칭키를 마스터 키로 사용함

### HTTP 는 Stateless (상태가 없는) 통신 프로토콜이라고 합니다. 따라서, 상태가 없다면 가령 HTTP 를 쓰는 서비스는 매번 로그인을 해 줘야 하거나 사용자 정보를 저장하는 일이 불가능합니다. 그런데 실제론 그렇지 않죠. 어떻게 이런 불편함을 해소했을까요?
* 세션 방식 사용

### 웹 브라우저에 https://www.google.com URL 을 입력 후 enter 를 쳤을 때 일어나는 과정을 최대한 상세하게 설명해주세요.

### HTTP(s) 프로토콜에서 바이너리 데이터를 전송하는 방식에 대해 설명해주세요.
바이너리 데이터를 전송하는 방식은 일반적으로 Base64 인코딩을 사용합니다. Base64는 6비트씩 데이터를 인코딩하여 8비트 ASCII 문자로 변환합니다. 이렇게 변환된 데이터는 텍스트 데이터처럼 전송될 수 있습니다.

HTTP(s) 프로토콜은 텍스트 데이터를 전송하는 데 최적화되어 있으므로, 텍스트 데이터를 전송하는 경우에는 별도의 인코딩이 필요하지 않습니다. 텍스트 데이터는 일반적으로 ASCII나 UTF-8 등의 문자 인코딩 방식으로 인코딩되어 전송됩니다.

### Socket 으로 웹 페이지를 크롤링하는 HTTP 클라이언트를 직접 구현해야 한다면, 어떻게 하시겠습니까?


# 목차
1. [Base64](#1-base64)
2. [난수와 의사난수, 진정한 난수를 생성하기 위한 방법](#2-난수와-의사난수-진정한-난수를-생성하기-위한-방법)
3. [컴퓨터는 어떤 요소들로 이루어져 있는가?](#3-컴퓨터는-어떤-요소들로-이루어져-있는가)
4. [프로그램과 프로세스](#4-프로그램과-프로세스)
5. [프로세스와 쓰레드](#5-프로세스와-쓰레드)
6. [멀티프로세싱, 멀티쓰레딩](#6-멀티프로세싱-멀티쓰레딩)
7. [교착상태(데드락)](#7-교착상태데드락)
8. [IPC](#8-ipc)
9. [스케줄링 알고리즘들](#9-스케줄링-알고리즘들)

## 1. Base64
### Base64란?
* Binary Data(이미지나 오디오)를 Text로 바꾸는 Encoding
* 8비트 이진 데이터(예를 들어 실행 파일이나, ZIP 파일 등)를 문자 코드에 영향을 받지 않는 공통 ASCII 영역의 문자들로만 이루어진 일련의 문자열로 바꾸는 인코딩 방식

#### 특징
* ASCII 중 제어문자와 일부 특수문자를 제외한 64개의 안전한 출력 문자만 사용
* 끝 부분의 Padding(==)으로 식별 가능
* 인코딩을 하게 되면 6bit당 2bit의 Overhead가 발생하여 전송해야 될 데이터의 크기가 약 33% 정도 늘어남

#### 사용이유
* ASCII는 7 bits Encoding인데 나머지 1bit를 처리하는 방식이 시스템 별로 상이함
* 따라서, ASCII로 인코딩하여 전송하게 되면 플랫폼에 따라 데이터에 영향이 끼침
* 플랫폼 독립적으로 바이너리 데이터를 전송할 필요가 있을 때 데이터의 손실을 막기 위해 사용

## 2. 난수와 의사난수, 진정한 난수를 생성하기 위한 방법
### 난수란?
* 정의된 범위 내에서 무작위로 추출된 수

### 의사난수란?
* 컴퓨터에 의해 생성된 모든 난수
* 시시각각 변하는 값을 초기값으로 잡고 여러 계산 과정을 거쳐 사람이 볼 때에 마치 임의의 값인 것처럼 보이게 하는 것

### 진정한 난수란?
* 재현 불가능한 난수
* ex) 동전던지기 (0과 1)

### 난수의 성질분류
* 무작위성
* 예측 불가능성
* 재현 불가능성

### 난수 특징
* 기본적으로 정해진 입력에 따라 정해진 값(결정적 유한 오토마타)

### 난수 생성 방법
* 시드(PRNG’s seed)라고 불리는 초기값을 기반으로 컴퓨터의 알고리즘으로 생성

## 3. 컴퓨터는 어떤 요소들로 이루어져 있는가?

### 소프트웨어와 하드웨어로 구성
#### 소프트웨어
*  컴퓨터에게 동작 방법을 지시하는 명령어 집합의 모임
  - 시스템 소프트웨어 : 응용 소프트웨어를 실행하기 위한 플랫폼을 제공하고 컴퓨터 하드웨어를 동작, 접근할 수 있도록 설계된 소프트웨어(운영체제, 컴파일러 등)
  - 응용 소프트웨어 : 사용자가 특정 작업을 수행 할 수 있도록 설계된 소프트웨어(Microsoft Office, Photoshop 등)

#### 하드웨어
* 컴퓨터를 구성하는 기계적 장치

#### 구성요소
![image](https://user-images.githubusercontent.com/41093183/195780269-58c2a2f2-b163-4219-8458-10ea44785659.png)


#### CPU (Central Processing Unit : 중앙처리장치)
* 메모리에 저장된 명령어를 읽어들여 수행하는 주체

  - ALU : 산술연산장치로 산술연산, 논리연산 등을 함
  - Control Unit : 명령어를 해석하여 ALU에 신호를 줌
  - 레지스터 : CPU안에 작은 메모리, 명령어들을 임시로 저장을함

#### Memory (기억장치)
* 명령어를 실행하기 위해 필요한 데이터와 상태, 명령어를 저장

  - CPU 레지스터(Register) : CPU 내 위치한 고속 메모리로 극소량의 데이터를 저장할 수 있음

  - 캐시(Cache) :SRAM 으로 구성되었으며, CPU Core 외에 존재하여 주기억장치와 CPU 간 속도차를 극복하기 위해 사용

  - 주 기억장치 : 현재 CPU가 처리하고 있는 내용을 저장하고 있는 기억 장치
    + ROM(Read Only Memory) : 전원이 끊어져도 기록된 데이터들이 소멸되지 않음(비휘발성 메모리)\
      컴퓨터를 키면 하드디스크에 저장된 운영체제를 메인 메모리에 적재하는 Boot loader가 이 ROM 영역에 할당되어 있음
    + RAM(Random Access Memory) : 읽고 쓰기가 가능하며, 휘발성 메모리임

  - 보조 기억장치 : 
    + HDD(Hard Disk Driver)
    + SDD(Solid State Driver)

* access 속도가 빠른 기억장치의 순서
  - 레지스터(Register) > 캐시(Cache) > 주기억장치(Main Memory) > 보조기억장치(HDD, SSD)

* 많은 용량을 지원하는 순서
  - 보조기억장치(HDD, SSD) > 주기억장치(Main Memory) > 캐시(Cache) > 레지스터(Register)


#### I/O Device (입출력 장치)
* 사용자 또는 컴퓨터 외부에서 데이터를 입력받고 출력하기 위한 장치

#### System bus (시스템 버스)
* 컴퓨터의 각 구성요소 간 데이터, 신호를 전달하기 위한 데이터 전달 경로
  - Address Bus : 메모리의 데이터를 읽거나 쓸 때 어느 위치에서 작업할 것인지를 알려주는 위치 정보
  - Data Bus : 다음에 어떤 작업을 할지 신호를 보내고 주소 버스가 위치 정보를 전달하면 데이터가 데이터 버스에 실려 목적지까지 이동
  - Control Bus : 다음에 어떤 작업을 할지 지시하는 제어 신호가 오고 


참조\
https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=dudwls251&logNo=220604910056\
https://lipcoder.tistory.com/202 [기록공간:티스토리]


## 4. 프로그램과 프로세스
### 프로그램이란?
* 특정 작업을 수행하는 일련의 명령어들의 모음
* 명령어들의 집합들로 그에 필요한 데이터를 묶어 놓은 파일

### 프로세스란?
* 실행중인 프로그램
* 메모리에 올라와 있는 프로그램

## 5. 프로세스와 쓰레드
### 프로세스란?
* 운영체제가 메모리 등의 필요한 자원을 할당해준 실행중인 프로그램

#### 특징
* 프로세스는 각각 Code, Data, Stack, Heap의 구조로 되어있는 독립된 메모리 영역을 할당 받음
* 각 프로세스는 별도의 주소 공간에서 실행되며, 서로 독자적인 메모리 공간을 갖기 때문에 서로 메모리 공간을 공유할 수 없음
* 다른 프로세스의 자원에 접근하려면 프로세스간의 통신(IPC)을 사용해야함
* 프로세스는 최소 하나 이상의 쓰레드를 포함

#### 구조
![process](https://user-images.githubusercontent.com/41093183/194826204-f11d50f1-6cb9-4e29-88fa-c53d40fbddb5.png)

* 코드 영역(code area) : 프로그래머가 작성한 프로그램이 코드 영역에 작성됨
* 데이터 영역(data area) : 코드가 실행되면서 사용한 변수나 파일들의 각종 데이터들이 모여있음
* 스택 영역(stack area) : 호출한 함수가 종료되면 되돌아올 메모리의 주소를 스택에 저장하거나 변수 사용 범위에 영향을 미치는 영역을 구현 할때 사용됨
* 힙 영역(heap area) : 동적으로 할당되는 데이터들을 위해 존재하는 공간 ex) malloc

### 쓰레드란?
* 프로세스 내의 하나의 실행 흐름 단위

#### 특징
* 각 쓰레드는 독자적인 스택(Stack) 메모리를 갖음
* 쓰레드는 프로세스 내에서 각각 스택만 할당받고 Code, Data, Heap 영역은 공유함
* 프로세스 내의 주소공간이나 자원들을 같은 프로세스 내의 쓰레드끼리 공유하며 실행
* 쓰레드는 메모리를 공유하기 때문에 동기화, 데드락 등의 문제가 발생 할 수 있음
* 한 쓰레드에 의해 다른 쓰레드가 영향 끼칠 수 있음 ex) Segmentation Fault

#### 구조
![thread2](https://user-images.githubusercontent.com/41093183/194827025-299980d1-e043-4eb8-8ed4-a53ee42a69e7.png)

* 쓰레드 ID ,PC ,레지스터 집합, 그리고 각자의 스택으로 구성

#### 스택을 쓰레드마다 독립적으로 할당하는 이유
* 스택 메모리 공간이 독립적이라는 것은 독립적인 함수 호출이 가능하다는 것이고 이는 독립적인 실행 흐름이 추가되는 것

#### 프로세스 대신 쓰레드를 사용하는 이유
* 프로세스보다 쓰레드 생성 비용이 적음(자원을 할당하는 시스템 콜이 줄어들어 효율적으로 관리할 수 있음)
* 프로세스 간의 통신보다 쓰레드 간의 통신의 비용이 적으므로 작업들 간의 통신의 부담이 줄어줄게 됨, 쓰레드는 Stack 제외하고 공유하고 있기 때문
* Context Switching의 비용이 프로세스보다 적음, 쓰레드는 Stack 영역만 처리하면 되기 때문

## 6. 멀티프로세싱, 멀티쓰레딩
### 멀티프로세싱이란?
* 하나의 응용프로그램을 여러 개의 프로세스로 구성하여 각 프로세스가 하나의 작업(태스크)을 처리하도록 하는 것
* 2개 이상의 프로세서들이 협력을 하여 작업을 병렬적으로 동시에 처리

#### 장점
* 여러 개의 자식 프로세스 중 하나에 문제가 발생하면 그 자식 프로세스만 죽는 것 이상으로 다른 영향이 확산되지 않음

#### 단점
* Context Switching 과정에서 캐쉬 메모리 초기화 등 무거운 작업이 진행되고 많은 시간이 소모되는 등의 오버헤드가 발생
* 프로세스 사이의 어렵고 복잡한 통신 기법(IPC)으로 프로세스는 각각의 독립된 메모리 영역을 할당받았기 때문에 하나의 프로그램에 속하는 프로세스들 사이의 변수를 공유할 수 없음

### 멀티쓰레딩이란?
* 하나의 응용프로그램을 여러 개의 쓰레드로 구성하고 각 쓰레드로 하여금 하나의 작업을 처리하도록 하는 것
* 프로세스 내부에 쓰레드가 2개 이상 존재하여 그 다수의 쓰레드들 간에 데이터 자원을 공유해 해당 프로세스가 실행시키고 있는 프로그램을 병렬적으로 처리

#### 장점
* 프로세스를 생성하여 자원을 할당하는 시스템 콜이 줄어들어 자원을 효율적으로 관리할 수 있음
* 쓰레드 사이의 작업량이 작아 Context Switching이 빠름
* 쓰레드는 프로세스 내의 Stack 영역을 제외한 모든 메모리를 공유하기 때문에 통신의 부담이 적음

#### 단점
* 주의 깊은 설계가 필요함
* 디버깅이 까다로움
* 단일 프로세스 시스템의 경우 효과를 기대하기 어려움
* 다른 프로세스에서 쓰레드를 제어할 수 없음 (즉, 프로세스 밖에서 쓰레드 각각을 제어할 수 없음)
* 멀티 쓰레드의 경우 자원 공유의 문제가 발생(동기화 문제)
* 하나의 쓰레드에 문제가 발생하면 전체 프로세스가 영향을 받음

## 7. 교착상태(데드락)
### 교착상태(데드락)란?
* 두 개 이상의 작업이 서로 상대방의 작업이 끝나기 만을 기다리고 있기 때문에 결과적으로 아무것도 완료되지 못하는 상태

#### 교착 상태의 조건
* 상호배제(Mutual exclusion) : 프로세스들이 필요로 하는 자원에 대해 배타적인 통제권을 요구함(자원 자체를 동시에 쓸 수 없는 경우)
* 점유대기(Hold and wait) : 프로세스가 할당된 자원을 가진 상태에서 다른 자원을 기다림
* 비선점(No preemption) : 프로세스가 어떤 자원의 사용을 끝낼 때까지 그 자원을 뺏을 수 없음
* 순환대기(Circular wait) : 각 프로세스는 순환적으로 다음 프로세스가 요구하는 자원을 가지고 있음

### 동기화란?
* 쓰레드들에게 하나의 자원에 대한 처리 권한을 주거나 순서를 조정해주는 기법

#### 사용이유
* race condition 이나 deadlock을 방지하기 위해


### 임계 구역(Critical Section)
* 병렬컴퓨팅에서 둘 이상의 쓰레드가 동시에 접근해서는 안되는 공유 자원을 접근하는 코드의 일부를 말함

### 동기화 방법
#### 스핀락(Spinlock)
* 임계 구역에 진입이 불가능할 때 진입이 가능할 때까지 루프를 돌면서 재시도하는 방식으로 구현된 락
* 임계 구역 진입 전까진 루프를 계속 돌고 있기 때문에 busy waiting이 발생
* 문맥 교환 비용이 들지 않으므로 효율을 높일 수 있지만 그 반대의 경우에는 다른 스레드에 cpu를 양보하지 않기 때문에 오히려 cpu 효율을 떨어뜨리게 됨
* 스핀 락은 문맥 교환이 일어나지 않기 때문에 멀티 프로세서 시스템에서만 사용 가능

#### 뮤텍스
* Locking 메커니즘으로 락을 걸은 쓰레드만이 임계 영역을 나갈 때 락을 해제할 수 있음
* 잠금 메커니즘이라는 점은 스핀 락과 동일하나 권한을 획득할 때까지 busy waiting 상태에 머무르지 않고 sleep 상태로 들어가고 wakeup 되면 다시 권한 획득을 시도하는 sleep lock을 사용

#### 세마포어
* Signaling 메커니즘으로 락을 걸지 않은 쓰레드도 signal을 사용해 락을 해제할 수 있음
* 하나의 쓰레드만 들어가게도 할 수 있고(binary semaphore), 여러개의 쓰레드가 들어가게 할 수도 있음(counting semaphore)

#### 모니터
* 하나의 객체마다 하나의 모니터를 결합하며, 결합된 객체가 동시에 두 개 이상의 쓰레드에 의해 접근할 수 없도록 lock을 걸음
* 하나의 프로세스내에 다른 쓰레드 간에 동기화할 때 사용됨

## 8. IPC
### IPC(Inter-Process Communication)란?
* 프로세스들 사이에 서로 데이터를 주고받는 행위 또는 그에 대한 방법이나 경로

#### 사용이유
* 프로세스는 완전히 독립된 실행 개체로 다른 프로세스의 영향을 받지않음
* 따라서, 서로간에 통신이 어려움. 이를 위해서 커널 영역에서 IPC라는 기능을 제공

#### 종류
* PIPE
* Named PIPE
* Message Queue
* Shared Memory
* Memory Map
* Socket

## 9. 스케줄링 알고리즘들 
### 스케줄링이란?
* 운영체제가 CPU의 자원을 어떤 프로세스에게 할당해 줄 지 결정하는 일

#### 사용이유
프로세스 간의 Context Switching 과정은 많은 자원 손실을 발생시킴, 따라서 이 일정을 어떻게 짰는지에 따라 CPU의 자원을 얼마나 효율적으로 사용하게 되는지가 결정

#### 목적
* CPU를 최대한 활용하기
* 대기 시간을 최소화 하기
* 처리량을 최대화 하기


### 스케줄링 알고리즘들 
----
#### FCFS(First Come, First Serve)
* 먼저 도착한 프로세스를 처리하는 스케줄링
* 비선점형 스케줄링
##### 단점
* convoy effect (소요시간이 긴 프로세스가 먼저 도착하여 효율성을 낮추는 현상)
----
#### SJF(Shorted Job First)
* 최단 작업을 우선하는 스케줄링
* 비선점형 스케줄링

##### 단점
* starvation(작업시간이 긴 프로세스가 CPU 할당을 계속 할당받지 못하는 현상)
----
#### Priority Scheduling
* 미리 주어진 프로세스의 우선 순위에 따라서 스케줄링하는 방식

##### 단점
* starvation

##### 해결방법
* agine (우선순위가 낮은 프로세스라도 오래 기다리면 우선순위를 높여줌)
----

#### RR(Round Robin)
* 가장 현대적인 CPU 스케줄링 방식
* 정해진 시간에 주어진 만큼 프로세스를 할당한 뒤 작업이 끝난 프로세스는 레디큐의 가장 마지막에 가서 재할당을 기다림
* Response time이 짧아짐

##### 단점
* time quantum(할당시간)이 너무 짧으면 Context Switch로 인하여 Overhead 발생, 너무 길면 FCFS와 같은 문제 발생할 수 있음
----
#### Multilevel-Queue
* 레디큐를 여러개의 큐로 분류하여 각 큐가 각각 다른 스케줄링 알고리즘을 가지는 방식
----

#### Multilevel-Feedback-Queue
* Multilevel-Queue는 특정 프로세스가 큐에 고정되어 있지만, Multilevel-Feedback-Queue는 큐와 큐 사이에 프로세스가 이동하는 것을 허용
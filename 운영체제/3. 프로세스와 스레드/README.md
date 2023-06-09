p. 164

## 3.3.4 PCB(Process Control Block)
운영체제에서 프로세스에 대한 메타데이터를 저장한 '데이터'. 프로세스 제어 블록이라고도 함.

프로세스가 생성되면 운영체제는 해당 PCB 생성.

 

PCB의 구조

-프로세스 번호(Process Identification Number, PID)

프로세스의 고유한 정소 번호. 다른 프로세스와의 구별을 위해 사용

-프로세스의 상태(Status)

준비, 실행, 대기, 보류 등의 상태를 나타냄.

-프로세스 권한

컴퓨터 자원 또는 I/O 디바이스에 대한 권한 정보

-프로그램 카운터 값

다음에 실행될 명령어의 주소값을 가지고 있음.

-CPU 레지스터

프로세스를 ㅅ실행하기 위해 저장해야 할 레지스터에 대한 정보

-CPU 스케줄링 정보

CPU 스케줄러에 의해 중단된 시간 등에 대한 정보

-계정 정보:

프로세스 실행에 사용된 CPU 사용량, 실행한 유저의 정보

-I/O 상태 정보

프로세스에 할당된 I/O 디바이스 목록

 

컨텍스트 스위칭(context switching)

PCB를 교환하는 과정. 한 프로세스의 할당된 시간이 끝나거나 인터럽트에 의해 발생.

문맥 교환을 위해 필요한 일의 양은 인터럽트 처리 전후의 프로세스가 같으냐, 다르냐에 따라 차이가 나는데 같을 때 해줄 일이 적음.

같을 경우(모드 스위칭, Mode Switching, 인터럽트 처리 위해 커널 모드로 처리 끝나면 사용자 모드로 바뀜.)는 인터럽트를 처리하는 동안 변경될 가능성이 있는 PCB의 일부분만 보관하면 됨

다를 경우(프로세스 스위칭, 인터럽트 처리 전후의 프로세스가 달라짐.)는 프로세스가 바뀌어 해주어야 할 일이 더 많아짐.

두 경우 모두 문맥 교환이 있으나 프로세스 스위칭일 때 해주어야 할 일이 기술적으로 더 요구되기 때문에 프로세스 스위칭을 문맥교환이라 하고, 모드 스위칭을 모드 스위칭이라고 부르기도 함.

 


https://velog.velcdn.com/images/ssongjh55/post/5fff97c0-f024-4e63-ace8-705b43f33879/image.png
A가 실행하다 멈춤.
A의 PCB 저장
B를 로드하여 실행
B의 PCB 저장
A의 PCB 로드
컨텍스트 스위칭이 일어날 때 유휴 시간 발생. 컨텍스트 스위칭의 비용에는 캐시미스도 있음.

 

유휴 시간(idle time)

컴퓨터가 작동 가능한데도 작업을 하지 아니하는 시간

(출처: https://wordrow.kr/%EC%9D%98%EB%AF%B8/%EC%9C%A0%ED%9C%B4%20%EC%8B%9C%EA%B0%84/)

 

비용: 캐시미스

컨텍스트 스위칭이 일어날 때 프로세스가 가지고 있는 메모리 주소가 그대로 있으면 잘못된 주소 변환이 새애기므로 캐시클리어 과정을 겪게 되고 이 때문에 캐시미스 발생

 

스레드에서의 컨텍스트 스위칭

스레드는 스택 영역을 제외하고 모든 메모리를 공유하기 때문에 스레드 컨텍스트 스위칭의 경우 비용이 더 적고 시간도 더 적게 걸림.

 

p. 166

## 3.3.5 멀티프로세싱
멀티프로세스(여러 개의 프로세스)를 통해 동시에 두 가지 이상의 일을 수행할 수 있는 것.

하나 이상의 일을 병렬로 처리할 수 있으며 특정 프로세스의 메모리, 프로세스 중 일부에 문제가 발생되더라도 다른 프로세스를 이용해서 처리할 수 있으므로 신뢰성이 높음.

 

멀티태스킹과 멀티프로세싱

-멀티태스킹: 단일 CPU에서 여러 응응 프로그램이 동시에 실행되는것처럼 보이도록 하는 시스템. 이 시스템이 구성돼야만 유튜브를 틀면서 기술 블로그를 작성하는 일을 할 수 있음.

-멀티 프로세싱: 멀티 프로세싱은 다중 CPU에 하나의 프로그램을 병렬로 실행해서 실행 속도를 극대화시킨다는 차이가 있음. 물론 CPU마다 여러 프로세스를 수행하게 하는 것은 덤.

(출처: https://velog.io/@redgem92/%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9C-CPU-%EC%8A%A4%EC%BC%80%EC%A5%B4%EB%A7%81-%EB%A9%80%ED%8B%B0-%ED%83%9C%EC%8A%A4%ED%82%B9-%EB%A9%80%ED%8B%B0-%ED%94%84%EB%A1%9C%EC%84%B8%EC%8B%B1-%EB%A9%80%ED%8B%B0-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D)

 

웹 브라우저

멀티프로세스 구조를 가지고 있음.

브라우저 프로세스: 주소 표시줄, 북마크 막대, 뒤로 가기 버튼, 앞으로 가기 버튼 등을 담당하며 네트워크 요청이나 파일 접근 같은 권한 담당
렌더러 프로세스: 웹 사이트가 '보이는' 부분의 모든 것을 제어함.
플로그인 프로세스: 웹 사이트에서 사용하는 플러그인 제어
GPU 프로세스: GPU를 이용해서 화면을 그리는 부분 제어
IPC(Inter Process Communication)

프로세스끼리 데이터를 주고받고 공유 데이터를 관리하는 메커니즘.

멀티프로세스는 IPC가 가능함.

메모리가 완전히 공유되는 스레드보다 속도가 떨어짐.

예) 클라이언트는 데이터를 요청하고 서버는 클라이언트 요청에 응답하는 것.

(참고하면 좋을 블로그: https://doitnow-man.tistory.com/110 )

 

공유 메모리(shared memory)

여러 프로세스에 동일한 메모리 블록에 대한 접근 권한이 부여되어 프로세스가 서로 통신할 수 있도록 공유 메모리를 생성해서 통신하는 것.

프로세스가 공유메모리 할당을 커널에 요청하면 커널은 해당 프로세스에 메모리 공간을 할당함. 이후 어떤 프로세스건 해당 메모리 영역에 접근할 수 있음.

메모리 자체를 공유하는 것이어서 불필요한 데이터 복사의 오버헤드가 발생하지 않아 (IPC 중) 가장 빠르며 같은 메모리 영역을 프로세스가 공유하기 때문에 동기화가 필요함.

하드웨어 관점에서 공유메모리는 CPU가 접근할 수 있는 RAM을 가리키기도 함.

(참고: https://jwprogramming.tistory.com/54)

 

파일

디스크에 저장된 데이터 또는 파일 서버에서 제공한 데이터. 이를 기반으로 프로세스 간 통ㅅ신.

파일을 통해 데이터를 주고받는 것. 문제가 많음.

실시간으로 직접 원하는 프로세스에 데이터 전달하기 어려움.

디스크에서 데이터 파일을 읽고, 프로세스에 load 되는 과정에서 컨텍스트 스위칭, 인터럽트 등 여러 일을 처리해야함.

(출처: https://velog.io/@redgem92/%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9C-IPC-%EA%B8%B0%EB%B2%95)

 

소켓

동일한 컴퓨터의 다른 프로세스나 네트워크의 다른 컴퓨터로 네트워크 인터페이스를 통해 전송하는 데이터를 의미. 

본래 네트워크 통신을 위한 기술.

소켓을 사용하면 로컬 컴퓨터 간의 통신 시 계층을 타고 내려가면서 송신을 하고, 아래 계층부터 위로 올라가서 대상 프로세스가 수신을 하는 방식

예) TCP와 UDP

(출처: https://velog.io/@redgem92/%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9C-IPC-%EA%B8%B0%EB%B2%95)

 

익명 파이프(unamed pipe)

프로세스간 FIFO 방식으로 읽히는 임시공간인 파이프를 기반으로 데이터를 주고받음.

단방향 방식의 읽기 전용, 쓰기 전용 파이프를 만들어서 작동하는 방식.

부모, 자식 프로세스 간에만 사용 가능. 다른 네트워크 상에서는 사용 불가.

부모 프로세스에서 자식프로세스로의 일방적 통신 기법

(출처: https://velog.io/@redgem92/%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9C-IPC-%EA%B8%B0%EB%B2%95)

 

명명된 파이프(named pipe)

파이프 서버와 하나 이상의 파이프 클라이언트 간의 통신을 위한 명명된 단방향 또는 양방향 파이프.

컴퓨터의 프로세스끼리 또는 네트워크상의 컴퓨터와도 통신 가능

 

메시지 큐

메시지를 큐 데이터 구조 형태로 관리하는 것을 의미.

커널의 전역변수 형태 등 커널에서 전역적으로 관리되며 다른 IPC 방식에 비해 사용방법이 매우 직관적이고 간단함.

다른 코드 수정 없이 코드 몇줄만 추가해 큐에 접근할 수 있음.

공유 메모리는 읽기 쓰기 빈도가 높으면 동기화 때문에 기능을 구현하는 것이 매우 복잡한데 그 대안으로 메시지 큐를 사용하기도 함.

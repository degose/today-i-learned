FDS-31-컴퓨터의 이해(운영체제,메모리,데이터베이스)
========


## VirtualBox

## 바이너리 에디터(iHex)
- 참고: <https://msdn.microsoft.com/ko-kr/library/cb4x6esf.aspx>
바이너리 편집기를 사용하면 16진수 또는 ASCII 형식으로 바이너리 수준에서 리소스를 편집할 수 있습니다. 또한 찾기 명령을 사용하여 ASCII 문자열 또는 16진수 바이트를 검색할 수도 있습니다. Visual Studio 환경에서 지원하지 않는 사용자 지정 리소스 또는 리소스 형식을 보거나 조금 변경해야 하는 경우에만 바이너리 편집기를 사용해야 합니다.
## 컴퓨터 언어가 2의 단위인 이유
- 모든 것이 비트단위. 효율적이니까

## 인터프리트 언어(Interpreted Language)
- 자바스크립트는 인터프린터 언어
- 컴파일러를 거쳐 기계어로 변환되지 않고 바로 실행되는 프로그래밍 언어를 말한다.
- 컴파일 언어의 종류 : Python, Ruby, Perl, PHP, JavaScript


## 컴파일 언어(Compile Language)
- 기계에 맞게 기계를 뱉어주는 것
- 프로그래머가 작성한 코드를 컴퓨터가 인식(저수준 언어로의 변환: 어셈블리어, 기계어등) 하기 위해 컴파일을 수행하고 이러한 컴파일 단계를 거쳐야 실행할수 있는 언어를 말한다.
- 컴파일 언어의 종류 : C, C++, Java, C#
- Code -> Compile -> Binary

## 플로피 디스크릐 논리적 구조
- 요즘은 하드디스크를 쓰지 않고 SSD를 쓴다.
- 디스크는 섹터 단위로 읽는다 (512바이트)
- 소프트웨어 단위 하드웨어 단위 나뉘어져 있는 이유? 

## FAT(File Allocation Table)
- 참고: <http://forensic-proof.com/archives/370>
- 다른 파일 시스템과 구별되는 점은 파일 내용을 클러스터 단위로 구성하고 이것을 링크드 리스트(Linked List)의 형태로 보관하는 것이다.
- 파일 할당 테이블
- 파일의 할당 정보를 표현한 테이블
- FAT 파일시스템은 크게 예약된 영역(Reserved Area), FAT 영역(FAT Area), 데이터 영역(Data Area)로 나눌 수 있다.
- 두 번째 FAT 영역은 첫 번재 테이블 영역이 손실되었을 경우 사용하기 위한 백업본이다. 따라서, 두 테이블 영역은 동일한 값이 저장되게 된다. 
- FAT 영역의 목적은 데이터 영역(Data Area)에 저장된 파일의 클러스터 할당 관계를 테이블 형태로 보여주는 것이다. FAT12/16은 2 바이트, FAT32는 4 바이트를 통해 데이터 영역의 시작 클러스터부터 마지막 클러스터까지 할당 관계를 표시한다. 다시 말해, 클러스터가 만약 4KB 크기를 가진다고 하면, FAT32에서는 각 클러스터가 FAT 영역의 4 바이트에 대응된다는 것이다.

## 파일시스템
- LBA(Logical Block Addressing)라는 주소 지정 방식을 사용할 경우 저장매체의 공간은 논리적으로 일렬로 쭉 늘어선 형태가 될 것이다. 이러한 논리적인 공간에 데이터를 읽고, 쓰고 하는 등의 관리를 위해 파일시스템이라는 좀 더 상위의 논리적인 구조를 사용한다. 

## 섹터단위
- 저장매체(하드디스크)의 물리적인 최소 단위는 1 섹터(512 바이트)이다. 따라서, 실제 하드디스크 컨트롤러에 의해 동작하는 단위도 섹터단위로 읽고 쓰여진다. 하지만 현대의 파일시스템들은 섹터단위로 데이터를 관리하지 않고, 여러 섹터를 묶은 클러스터라는 개념으로 데이터를 관리한다. 이는 평균적인 파일 크기가 커진 상황에서 섹터 단위로 관리하는 것은 비효율적이기 때문이다.

## 글리스터(Cluster)
- 참고: <http://cappleblog.co.kr/137>
- 하드디스크 위에 파일을 저장하는 논리적 단위이며, 컴퓨터의 운영체계에 의해 관리된다. 
- 파일이 하드디스크에 저장되면 적어도 하나 이상의 클러스터를 차지하게 되며, 아주 커다란 파일인 경우 여러 개의 클러스터에 걸쳐 저장되는 수도 있다.

## 논리 게이트
- 참고: <http://ocw.dongyang.ac.kr/cms_ocw/electsystem/3791/note/5_03.pdf>
### 논리회로
- AND : 모든 입력들이 1인 경우는 출력이 1이 되고, 그 이외의 입력 조합에 대해서는 출력이 0이 되는 논리 게이트이다. 
- NOT : 입력을 반전시켜 출력이 되게 하는 게이트이다. 즉, 입력이 1(= H)이면 출력이 0(= L)이 되게 하고, 입력이 0이면 출력이 1이 되게 하는 논리 게이트이다. 
- OR : 입력들 중 어느 한 입력이라도 1인 경우는 출력이 1이 되고, 입력들이 모두 0인 경우만 출력이 0이 되는 논리 게이트이다.
- NAND, NOR, XOR(exclusiveOR), XNOR(exclusive NOR)
- NAND 하나로 AND, OR, NOT을 다 만들 수 있다.
- 그냥 OR도 NAND 3개로 만든 OR도 똑같은 OR
- 추상화의 중요성!
- 결국 사람이기 때문에 복잡한 생각을 못함 => 그러므로 단순화 시켜야 한다.
- 결과 값이 같다면 과정이 달라도 같은 것이라고 생각할 수 있어야 한다.
- context에 민감해져야 한다.
- 언어의 발달 순서 = 추상화의 발달 순서

## CPU
### 진공관, 트렌지스터
- 컴퓨터와 무슨관련? => 스위치 직렬방식: AND게이트, 병렬방식: OR게이트
### 반가산기(Half Adder) 설계
- 두 개의 한자리 2진 숫자 A와 B를 더하여 합 (sum: S)과 자리올림 (carry: C)의 두 개의 출력을 얻는 회로이다. 
### 전가산기(Full adder) 설계
- 전가산기는 두 자리 이상의 2진수를 더할 경우 입력의 가수, 피가수 및 자리 올림수가 더해지고 합과 자리올림을 출력하는 회로이다. 

## 폰노이만 구조
- [CPU], [메모리], [프로그램] 구조를 갖는 범용 컴퓨터 구조의 확립, 세계 최초의 프로그램 내장 방식 컴퓨터 EDSAC을 제작
- 내장 메모리 순차 처리방식
- 하드웨어: 정적이고 변하지 않는 게이트 / 소프트웨어: 우리 의도데로 값을 바꿀 수 있다.
- 메모리와 데이터가 구분되어 있지 않고 하나의 버스를 가지고 있음
- 하버드 구조 : 메모리와 데이터의 버스가 구분되어 있다.

## 레지스터와 메모리
- 둘 다 데이터를 저장하는 역할
- 레지스터는 cpu 안에 있는것, ram은 cpu밖에 있다.
- 병목현상
- 병목현상을 최대한 줄이면서 코딩하는 방법을 알아야 한다.

## 클럭(clock signal)
- 매 클럭시마다 머신(cpu)의 상태는 변화됨
- CISC(Complex Instruction Set Computer)
- RISC(Reduced Instruction Set Computer) - 회로가 안 복잡
- 논리상태 H(high,논리 1)와 L(low,논리 0)이 주기적으로 나타나는 방형파 신호
- 전자공학의 디지털 회로에서 클럭 신호에 맞추어 신호의 처리를 하는 동기 처리를 위해 사용한다.
- 클럭은 순차회로의 플립플럽에서 반드시 필요하다. 여러개의 플럽플럽이 비동기 클럭으로 동작하더라도 클럭입력은 필요하다. 논리 회로가 커지면 여러개의 클럭이 필요하므로 동기와 비동기 섞여 설계되어 동작한다. 
- SX / DX 차이 : FPU(Floating Point Unit) 유무 FPU가 있으면 한클럭이면 소숫점 연산이 끝남

## Instruction
- 참고: <http://oukene.tistory.com/4>
- 인스트럭션은 컴퓨터가 어느 정보를 가지고 어떠한 처리를 하는가를 나태난다.
- 인스트럭션 내에 포함되는 정보
      - 연산자(operation code : OP-code)
      - 피 연산자(operand)
- 인스트럭션을 주 기억장치에서 읽는 것을 인스트럭션 펫치(Instruction fetch : IF)
- 피연산자를 주기억 장치에서 읽는 것을 피연산자 펫치(operand fetch : OF)라 부른다.

## 비트 연산자
- & : 비트 단위의 AND 연산자(&)는 첫 번째 피연산자의 각 비트를 두 번째 피연산자의 해당 비트와 비교한다. 양쪽 비트가 모두 1이면 해당 결과 비트는 1로 설정된다. 그렇지 않으면 해당 결과 비트는 0으로 설정된다.
- ^ : 비트 단위의 독점적 OR 연산자(^)는 첫 번째 피연산자의 각 비트를 두 번째 피연산자의 해당 비트와 비교한다. 한 비트가 0이고 다른 비트가 1인 경우 해당 결과 비트는 1로 설정된다. 그렇지 않으면 해당 결과 비트는 0으로 설정된다.
- | : 비트 단위의 독점적 OR 연산자(^)는 첫 번째 피연산자의 각 비트를 두 번째 피연산자의 해당 비트와 비교한다. 어느 한쪽 비트가 1이면 해당 결과 비트는 1로 설정된다. 그렇지 않으면 해당 결과 비트는 0으로 설정된다.

## 동기, 비동기
- 동기(syncronization)는 대상이 클럭에 의존함
- 비동기는 클럭에 의존하지 않음
- 블록 / 논블록(자바스크립트 콜)과 유사

## 인터럽트
- 참고: <http://raisonde.tistory.com/267>
- 프로그램을 실행 중에 이슈가 발생하면 현재 작업을 중단하고 발생된 상황을 처리한 후 다시 작업으로 복귀하는 것
- 내부 인터럽트 / 외부 인터럽트 / 소프트웨어 인터럽트

## 캐시 메모리
- 참고: <http://it.donga.com/215/>
- 속도가 빠른 장치와 느린 장치 사이에어 속도 차에 따른 병목 현상을 줄이기 위한 범용 메모리를 말한다.

## I/O(입출력 시스템)
- 참고: <http://cs.sch.ac.kr/lecture/os/2015/15-13-OS-IOSystem.pdf>

## 버스
- 데이터를 통신할 수 있게 해주는 시스템
- system bus : cpu와 메모리를 연결하는 subsystem
- i/0 bus : 메모리와 다른 입출력 장치와 통신을 하는 subsystem
- address / data / control




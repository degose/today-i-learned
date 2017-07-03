FDS-37-자료구조
========

- 참고: <http://www.geeksforgeeks.org/>
- 참고: <http://codingdojang.com/>
- 책 추천: [코딩 인터뷰 완전분석]

- 우리코드 -> 프레임 워크 -> 브라우저 엔진 -> 운영체제 -> 하드웨어
- 우리는 가장 끝단에 있다.(가장 위에)

# 자료구조
- 참고: <http://boycoding.tistory.com/32>
- 자료를 효율적으로 이용할 수 있도록 컴퓨터에 저장하는 방법
- 어떤 자료를 어떻게 사용하느냐에 따라 용량과 프로그램 실행속도가 달라진다.

## ADT(Abstract Data Type) 
- 추상자료형
- 실제 자료가 내부적으로 어떻게 돌아가는지에 대해서는 따지지 않고, 이 자료가 하는 기능에 대해서만 이야기하는것.(객체지양)
- ADT의 예
  - 스택(Stack): FILO(First In Last Out)/LIFO(Last In First Out)의 자료구조로, 마지막에 입력된 데이터가 먼저 출력되는 자료구조이다.
  - 큐(Queue): 큐는 FIFO(First In First Out)의 자료구조로, 먼저 입력된 데이터가 먼저 출력되는 자료구조이다.
  - 데크(Degue): 양쪽에서 넣고 뺄 수 있는 일반적인 선형구조.
- data:물 / data type: 주전자 / abstract data type: 
- 데이터의 선언
- 연산의 선언

## 배열(Array)
- 구체적인 자료구조
### 구체적(Concrete) vs 추상적(Abstract)
- 컴퓨터는 계속 추상화 해왔다.
- 결국 사람이 만들기 때문에 추상화가 가지는 장점은 어마어마하다.
- 선으로 공간을 확보하고, 규칙적이다.
- 데이터는 주소값을 갖는다. 주소값은 고정
### 다차원 배열
- 1차원 배열 : (0)(1)(2)(3)
- 2차원 배열 : 좌표값처럼 (0,0)(1,0)(2,0)
```js
var a = [[1,2,3],[4,5,6],[7,8,9]]
```
- 참고: <http://ropas.snu.ac.kr/~gslee/lecture-slides/c2011-01/20110513-01.pdf>

### REPL session
- 참고: <https://velopert.com/235>
- Read Eval Print Loop
- 사용자가 커맨드 값을 입력하면 시스템이 값을 반환하는 환경
```bash
$ node [파일이름].js
```


## 해쉬테이블(hash table)
- 자바스크립트에서는 오브젝트를 해쉬테이블처럼 쓰기도 하지만 엄밀히 말하면 다르다.
- 정말 많이 쓰이는 자료구조
- key, value 가 pair(쌍)를 이룬다.
- burkets (바구니) -> 값을 담는다.

## 포로토타입(prototype)
- 원형. 원래의 상태
- 생성자함수 -> 어떤 객체가 생성됐을때 호출되는 함수
- this
- 오버라이드: 재정의

## 포인터(pointer)
- 다른 변수, 혹은 그 변수의 메모리 공간주소를 가리키는 변수를 말한다.
- 포인터가 가리키는 값을 가져오는 것을 역참조라고 한다.

### 프리미티브 타입, 레퍼런스 타입
- 참고: <http://jdm.kr/blog/213>
- primitive type(기본형) vs reference type(참조형)

## 세션과 쿠키
- 서버 안에 세션 아이디가 있다.
- 서버와 클라이언트가 통신할 때 세션아이디를 이용한다.

## 재귀호출(recursive call)
### 재귀함수


## 빅오 표기법(Big O notation)
- 참고: <https://ko.khanacademy.org/computing/computer-science/algorithms#asymptotic-notation>
- 복잡도(complexity)
- 알고리즘에서 최악의 성능을 표시
- "O표기법에서 상수의 존재는 알고리즘의 성능에 아무런 영향을 끼치지 못한다"
- 시간 복잡도, 공간 복잡도 -> 서로 트레이드오프 -> 
- input기준으로 데이터에 따라 출력 결과가 얼마큼 걸리냐? (비례)
- 입력량과의 관계(비례의 정도)
```js
O(logn)
log10 = 100 = 2
log10 = 10 22 = 22
```

## 리스트(List or Sequence)
- 시퀀스 -> 수학에서 수열 같은 것 -> 리스트는 시퀀스보다 더 상위 개념
- 리스트 -> 링크드리스트(Linked List) / 어레이 리스트(Array List)
- 어레이는 리스트라 할 수 있지만 리스트는 어레이라고 할 수 없다.
- 원소의 순서(order) 존재
- 인터페이스
- add, next

```js
var LinkedList = function(head) {
  this.head = head
}

LikedList.prototype.add = function(linkedNode) {

  var currentNode = this.head;
  while(currentNode.nextNode != null) {
    currentNode = currentNode.nextNode
  }
  currentNode.nextNode = linkedNode
}

var LinkedNode = function(value) {
  this.nextNode = null
  this.value = value
}

LinkedNode.prototype.next = function() {
  return this.nextNode
}

LinkedList.prototype.get = function() {
  var count = 0;
  var currentNode = this.head;
  while(count++ != index) {
    console.log(currentNode)
    currentNode = currentNode.nextNode
  }
  return currentNode
}

var nodeA = new LinkedNode("a")
var nodeB = new LinkedNode("b")
var nodeC = new LinkedNode("c")

var linkedList = new LinkedList(nodeA)
linkedList.add(nodeB)
linkedList.add(nodeC)

// 이게 모카 같은 테스트 프레임워크 등
// TDD 테스트 주도 기반
var result = linkedList.get(2)
console.log(result)

if(result.value === 'c') {
  console.log('test passed')
} else {
  console.log('test fail')
}
```
## 스택(stack)
- LIFO(Last In First Out)
- 마지막 들어온 것이 먼저 나간다.
- 메서드
  - push
  - pop
- 새로운 context를 만들고 다시 예전 context를 되돌려야 할때 쓰는 자료구조
- 스택오버플로우(stack overflow)
- 스택언더플로우(stack underflow)
- 스텍 프레임(stack frame) -> 덩어리 -> 각종 레지스터, 지역변수 정보

## 큐(queue)
- FIFO(First In First Out)
- 먼저 들어온 것이 먼저 나간다.
- 메서드
  - enqueue
  - dequeue
- 대기표 시스템 같은곳에서 유용
- overflow / underflow
- 환형큐(circular queue) - 구현
- 우선순위큐(priority queue)

## 트리(tree)
- 계층구조를 표현하는 자료구조
- root - parent - child 
- siblings
- leaf(잎)노드 - 자식이 없는 노드
- depth(깊이), height of tree
- complete binary tree(완전 이진 트리)
### 이진트리(binary tree)
- 자식이 기껏해야 2개인 것
- 완전 이진트리: 각 끝에 있는 leaf노드에
- 이진 탐색 트리
  - AVL-tree
  - Red-black tree
  - 완전 이진트리를 유지하기 위한 방법
- 쓰레드 이진 트리
- 힙(heap): 루트가 최대값이나 최소값??
### B트리
### 트라이
- 색인할 때

## 그래프(graph)
- 방향그래프(directed graph) / 무방향그래프(undirected graph)
- 정점(vertex)
- 변(edge)
- 차수(degree)
- 인접리스트(adjacency list)
- 인접 행렬(adjacency matrix)

## 탐색(search)
### 깊이 우선 탐색(depth-first search)
- stack
- 재귀호출 사용
- BFS보다 코드가 상대적으로 단순
### 너비 우선 탐색(breadth-first search)
- queue
- while 루프 사용 -> stack overflow 위험성 없음
- BFS보다 코드가 복잡

## 정렬(sort)
- 참고: <http://hsp1116.tistory.com/33>
- 추가 / 삭제
- 힙정렬 : 가장 크거나 가장 작은 것

## 알고리즘
- 모델링
- 참고: <https://goo.gl/8rxm3J>
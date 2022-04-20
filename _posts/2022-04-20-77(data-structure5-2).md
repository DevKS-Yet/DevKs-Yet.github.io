---
title: "우선순위 큐"
excerpt: "PriorityQueue"

categories:
- Data-Structure

tags:
- data structure
- data
- structure
- dynamic
- queue
---

# 자료 구조 목차

- Data-Structure
  - Linear
    - Static
      - Array
    - Dynamic
      - Linked List
      - Stack
      - Queue
  - Non Linear
    - Tree
    - Graph


## 자바에서의 우선순위 큐(PriorityQueue)

일반적으로 큐는 FIFO의 구조를 가진다. 하지만 PriorityQueue는 먼저 들어온 순서대로 나가는 것이 아니라 우선순위가 높은 순으로 먼저 나가게 된다.

아래는 ASCII 값이 가장 높은 요소가 먼저 나가도록 한 PriorityQueue의 실행 순서이다.

![About PriorityQueue](/assets/images/2022/about-priorityQueue.png)

###### PriorityQueue가 상속받는 것들

- Serializable
- Queue<E>
- Collection<E>
- Iterable<E>

###### PriorityQueue의 중요 포인트 :

- PriorityQueue는 null을 허용하지 않는다
- PriorityQueue를 비교불가한 객체로는 생성할 수 없다(이런 에러 발생 : `cannot be cast to class java.lang.Comparable`)
- PriorityQueue는 무한(unbound) 큐이다
- 이 큐의 head는 특정 순서에 의해 정해진 최적의 요소이다. 만약 다수의 요소가 least value라면 head는 다수의 요소 중 하나이다
- PriorityQueue는 thread-safe 하지않음으로 자바에서는 `BlockingQueue` 인터페이스를 상속받는 `PriorityBlockingQueue`를 제공한다
- 큐의 retrieval(검색) 작업은 큐의 head 요소 access, poll, remove, peek 한다
- add와 poll 메서드는 O(log(n))의 시간이 필요하다
- PriorityQueue는 `AbstractQueue`, `AbstractCollection`, `Collection` 그리고 `Object` 클래스의 메서드를 상속받는다

#### PriorityQueue 생성하기

- PriorityQueue()  :  
PriorityQueue의 기본 capacity인 11로 생성한다

```java
PriorityQueue<E> pq = new PriorityQueue<E>();
```

- PriorityQueue(Collection<E> c) :  
특정 콜렉션의 요소를 담는 PriorityQueue를 생성한다

```java
PriorityQueue<E> pq = new PriorityQueue<E>(Collection<E> c);
```

- PriorityQueue(int initialCapacity) :  

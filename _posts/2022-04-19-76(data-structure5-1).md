---
title: "자바에서의 큐"
excerpt: "Queue In Java"

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


## 자바에서의 큐 인터페이스에 대해

큐에 대한 개념을 알아보았으니 자바에서 사용되는 큐에 대해서 알아보자  
큐 인터페이스는 `java.util` 패키지 안에 있으며 콜렉션 인터페이스에서 FIFO(First In First Out) 순으로 실행하는 요소들을 상속받고 있다.

![Hierarchy-of-the-Queue-Interface](/assets/images/2022/hierarchy-of-the-Queue-Interface.png)

인터페이스임으로 큐는 선언을 위한 구현 클래스가 필요하다. 자주 사용되는 구현 클래스로는 `PriorityQueue`와 `LinkedList`가 있다. 참고로 이 클래스들은 thread safe하지 않습니다. 만약 thread safe가 필요하다면 `PriorityBlockingQueue`을 상속 받는 걸을 추천한다.

###### 큐 객체 선언 및 생성

자바 1.5부터 소개된 제네릭이 생긴 이후부터큐에 어떤 타입의 객체를 담을건지 제한을 둘 수도 있다.
```java
Queue<Obj> queue = new PriorityQueue<Obj>();
```

###### 큐 예제(Linked List) :

```java
import java.util.LinkedList;
import java.util.Queue;

public class QueueSample1 {
    public static void main(String[] args) {
        Queue<Integer> integerQueue = new LinkedList<>();
        
        // adds elements {0, 1, 2, 3, 4} to the queue
        for (int i=0; i<5; i++) {
            integerQueue.add(i);
        }
        
        // queue dispaly
        System.out.println("Elements fo queue : " + integerQueue);
        
        // remove the head of queue
        int removedElement = integerQueue.remove();
        System.out.println("removed element : " + removedElement);
        
        System.out.println(integerQueue);
        
        // view the head of queue
        int head = integerQueue.peek();
        System.out.println("head of queue : " + head);
        
        int size = integerQueue.size();
        System.out.println("Size of queue : " + size);
    }
}
```

###### 큐 인터페이스 명령어(PriorityQueue)

1. 요소 더하기


---
title: "데크 인터페이스"
excerpt: "Deque Interface"

categories:
- Data-Structure

tags:
- data structure
- data
- structure
- dynamic
- deque
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


## 데크 인터페이스(Deque Interface)

데크 인터페이스는 java.util 패키지 안에 있는 queue interface의 서브타입이다.
데크는 `double-ended queue`의 약자이며 큐 임에도 불구하고 head가 아닌 rear에 있는 요소 삽입 또는 삭제가 가능하다.
그러므로 FIFO(queue)나 LIFO(stack)로 사용이 가능하다.

![hierarchy of the queue interface](/assets/images/2022/hierarchy-of-the-Queue-Interface.png)

데크는 인터페이스임으로 생성할 시에 구현체 클래스로 생성을 해야한다.

###### 데크 예시

```java
import java.util.*;

public class DequeSample {
    public static void main(String[] args) {
        Deque<String> deque = new LinkedList<String>();
        
        deque.add("Element 1 (Tail)");
        
        deque.addFirst("Element 2 (Head)");
        
        deque.addLast("Element 3 (Tail)");
        
        deque.push("Element 4 (Head)");
        
        deque.offer("Element 5 (Tail)");
        
        deque.offerFirst("Element 6 (Head)");
        
        System.out.println(deque);
        
        deque.removeFirst();
    }
}
```
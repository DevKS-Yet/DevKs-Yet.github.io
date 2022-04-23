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
        deque.removeLast();
        System.out.println("Deque after removing first and last : " + deque);
    }
}
```

### ArrayDeque 클래스를 이용한 Deque Interface

###### 요소 추가하기

```java
import java.util.*;

public class DequeSample1 {
    public static void main(String[] args) {
        Deque<String> stringDeque = new ArrayDeque<String>();
        
        stringDeque.add("World");
        stringDeque.addFirst("Hello");
        stringDeque.addLast("Java");
        
        System.out.println(stringDeque);
    }
}
```

###### 요소 제거하기

```java
import java.util.*;

public class DequeSample2 {
    public static void main(String[] args) {
        Deque<String> stringDeque = new ArrayDeque<String>();
        
        stringDeque.add("World");
        stringDeque.addFirst("Hello");
        stringDeque.addLast("Java");
        
        System.out.println(stringDeque);
        
        System.out.println(stringDeque.pop());
        
        System.out.println(stringDeque.poll());
        
        System.out.println(stringDeque.pollFirst());
        
        System.out.println(stringDeque.pollLast());
    }
}
```

###### 데크 내부 순회하기(iterating)

```java
import java.util.*;

public class DequeSample3 {
    public static void main(String[] args) {
        Deque<String> stringDeque = new ArrayDeque<String>();
        
        stringDeque.add("World");
        stringDeque.addFirst("Hello");
        stringDeque.addLast("Enjoy");
        stringDeque.add("Java!");
        
        for (Iterator itr = stringDeque.iterator(); itr.hasNext();) {
            System.out.print(itr.next() + " ");
        }
        
        System.out.println();
        
        for (Iterator itr = stringDeque.descendingIterator(); itr.hasNext();) {
            System.out.print(itr.next() + " ");
        }
    }
}
```

> 이것으로 데크(deque)까지 알아보았다. 데크는 인터페이스임으로 데크를 구현하는 클래스가 ArrayDeque 이외에도 많으니 ArrayDeque로만 고집해서 사용하지 않았으면 좋겠다.
> 원래는 데크 구현체 클래스까지 할려고 했다가 너무 많은듯하여 논리니어 자료 구조로 빠르게 넘어가겠다.
> 
> 부족한 것이 있다면 메일이나 댓글을 남겨주면 추가 또는 수정을 할테니 언제든지 환영이다!


### References

- [https://www.geeksforgeeks.org/arraydeque-in-java/?ref=lbp](https://www.geeksforgeeks.org/arraydeque-in-java/?ref=lbp)
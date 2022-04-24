---
title: "배열 데크"
excerpt: "ArrayDeque"

categories:
- Data-Structure

tags:
- data structure
- data
- structure
- dynamic
- array
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


## 배열 데크(ArrayDeque)

이전 포스팅에서 데크 인터페이스에 대해서 설명하며 배열 데크 구현체를 이용한 데크 인터페이스를 알아보았다.
이번 포스팅에서는 배열데트에 대해서 알아 볼 것이다.

아래는 배열데크의 중요한 특징이다.

- 배열데크는 수용(size)에 대한 제한이 없으며 필요한 사용량 만큼 커진다
- 배열데크는 외부 동기화가 존재하지 않기에 thread-safe하지 않는다. 또한 멀티 쓰레드에 의한 concurrent access를 지원하지 않는다
- 배열데크에는 null 요소를 넣을 수 없다
- 배열데크 클래스를 스택으로 사용할 시 `Stack` 클래스보다 빠르다
- 배열데크 클래스를 큐로 사용할 시 `LinkedList`보다 빠르다

> 중요 특징 중에 stack과 queue 용도로 사용 시 빠르다는 것이 매우 중요해보인다

### 배열데크에 상속된 인터페이스 :

배열데크는 두 개의 인터페이스를 상속 받는다. 두 개는 아래와 같다

- Queue Interface : FIFO의 원리를 지닌 인터페이스
- Deque Interface : 양 쪽에서 삽입 및 제거가 가능한 인터페이스. 큐 인터페이스를 상속 받는다

배열데크는 큐와 데크를 상속받는다. 양 쪽에서 동적으로 resizable이 가능하다.
또한 배열데크 계층에는 `Serializable`, `Clonable`, `Iterable<E>`, `Collection<E>`, `Deque<E>`, `Queue<E>`가 있다.

![hierarchy of the ArrayDeque](/assets/images/2022/hierarchy-of-the-ArrayDeque.png)

### 배열데크 선언 및 생성

- `ArrayDeque()` : 초기 용량은 16 요소인 빈 배열데크 생성

```java
ArrayDeque<E> dq = new ArrayDeque<E>();
```

- `ArrayDeque(Collection<? extends E> c)` : 특정 콜렉션에 있는 엘레멘트로 배열데크 생성

```java
ArrayDeque<E> dq = new ArrayDeque<E>(Collection col);
```

- `ArrayDeque(int numofElements)` : 특정 용량의 빈 배열데크 생성

```java
ArrayDeque<E> dq = new ArrayDeque<E>(int numofElements);
```

#### 배열데크 예시

```java
import java.util.*;

public class ArrayDequeSample {
    public static void main(String[] args) {
        Deque<Integer> integerDeque = new ArrayDeque<>(10);
  
        integerDeque.add(10);
        integerDeque.add(20);
        integerDeque.add(30);
        integerDeque.add(40);
        integerDeque.add(50);
  
        for (Integer element : integerDeque) {
            System.out.println("Element : " + element);
        }
  
        System.out.println("Using clear()");
        integerDeque.clear();
  
        integerDeque.addFirst(1);
        integerDeque.addFirst(2);
  
        integerDeque.addLast(9);
        integerDeque.addLast(8);
  
        System.out.println("Above elements are removed now");
  
        System.out.print("Elements of deque using Iterator : ");
        for (Iterator itr = integerDeque.iterator(); itr.hasNext();) {
            System.out.print(itr.next() + "\t");
        }
        System.out.println();
  
        System.out.print("Elements of deque in reverse order : ");
        for (Iterator dItr = integerDeque.descendingIterator(); dItr.hasNext();) {
            System.out.print(dItr.next() + "\t");
        }
        System.out.println();
  
        System.out.println("Head Element Using element() : " + integerDeque.element());
        System.out.println("Head Element Using getFirst() : " +integerDeque.getFirst());
        System.out.println("Last Element using getLast() : " + integerDeque.getLast());
  
        Object[] arr = integerDeque.toArray();
        System.out.println("Array Size : " + arr.length);
  
        System.out.print("Array elements : " );
        for (int i=0; i<arr.length; i++) {
            System.out.print(arr[i] + "\t");
        }
        System.out.println();
  
        System.out.println("Head element : " + integerDeque.peek());
  
        System.out.println("Head element poll : " + integerDeque.poll());
  
        integerDeque.push(10);
        integerDeque.push(15);
        integerDeque.push(20);
  
        System.out.println("Head element remove : " + integerDeque.remove());
  
        System.out.println("The final array is : " + integerDeque);
    }
}
```
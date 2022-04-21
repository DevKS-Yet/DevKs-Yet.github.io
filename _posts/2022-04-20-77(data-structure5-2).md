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

- `PriorityQueue()`  :  
PriorityQueue의 기본 capacity인 11로 생성한다

```java
PriorityQueue<E> pq = new PriorityQueue<E>();
```

- `PriorityQueue(Collection<E> c)` :  
특정 콜렉션의 요소를 담는 PriorityQueue를 생성한다

```java
PriorityQueue<E> pq = new PriorityQueue<E>(Collection<E> c);
```

- `PriorityQueue(int initialCapacity)` :  
초기 capacity를 주어 PriorityQueue를 생성한다

```java
PriorityQueue<E> pq = new PriorityQueue<E>(int initialCapacity);
```

- `PriorityQueue(int initialCapacity, Comparator<E> comparator)` :  
초기 capacity와 정의한 comparator의 순서대로 저장하는 PriorityQueue를 생성한다

```java
PriorityQueue<E> pq = new PriorityQueue(int initialCapacity, Comparator<E> comparator);
```

- `PriorityQueue(PriorityQueue<E> c)` :  
요소를 담고 있는 특정한 PriorityQueue로 PriorityQueue를 생성한다

```java
PriorityQueue<E> pq = new PriorityQueue(PriorityQueue<E> c);
```

- `PriorityQueue(SortedSet<E> c)` :  
요소를 담고 있는 특정한 SortedSet으로 PriorityQueue를 생성한다

```java
PriorityQueue<e> pq = new PriorityQueue<E>(SortedSet<E> c);
```

#### PriorityQueue 기본 수행 작업 :  

- boolean add(E element) : 특정 요소를 priority queue에 삽입
- public peek() : queue의 head를 찾아서 제거하지않고 값을 반환한다. 큐가 비어있다면 null 반환
- public poll() : queue의 head를 찾아서 제거 및 값을 반환한다. 큐가 비어있다면 null 반환

```java
import java.util.*;

class PriorityQueueSample {
    public static void main(String[] args) {
        // Creating empty priority queue
        PriorityQueue<Integer> integerPriorityQueue = new PriorityQueue<>();
        
        // Adding items to the integerPriorityQueue using add()
        integerPriorityQueue.add(10);
        integerPriorityQueue.add(20);
        integerPriorityQueue.add(15);
        
        // Printing the top element of PriorityQueue
        System.out.println(integerPriorityQueue.peek());
        
        // Printing the top element and removing it from the PriorityQueue container
        System.out.println(integerPriorityQueue.poll());
        
        // Printing the top element again
        System.out.println(integerPriorityQueue.peek());
    }
}
```

#### PriorityQueue 명령어

Priority Queue 클래스에서 자주 사용되는 명령어(메서드)를 실행했을 시 변화되는 것을 알아보자

- 요소 추가하기

```java
import java.util.*;
import java.io.*;

public class PriorityQueueSample1 {
    public static void main(String[] args) {
        PriorityQueue<String> stringPriorityQueue = new PriorityQueue<>();
        
        stringPriorityQueue.add("Hello");
        stringPriorityQueue.add("World");
        stringPriorityQueue.add("Java");
        System.out.println(stringPriorityQueue);
    }
}
```

- 요소 제거하기

```java
import java.util.*;
import java.io.*;

public class PriorityQueueSample2 {
    public static void main(String[] args) {
        PriorityQueue<String> stringPriorityQueue = new PriorityQueue<>();
        
        stringPriorityQueue.add("Hello");
        stringPriorityQueue.add("World");
        stringPriorityQueue.add("Java");
        
        System.out.println("Initial PriorityQueue : " + stringPriorityQueue);
        
        stringPriorityQueue.remove("Hello");
        
        System.out.println("After Remove : " + stringPriorityQueue);
        
        System.out.println("Poll Method : " + stringPriorityQueue.poll());
        
        System.out.println("Final PriorityQueue : " + stringPriorityQueue);
    }
}
```

- 요소 갖고오기

```java
import java.util.*;

public class PriorityQueueSample3 {
    public static void main(String[] args) {
        PriorityQueue<String> stringPriorityQueue = new PriorityQueue<>();
        
        stringPriorityQueue.add("Hello");
        stringPriorityQueue.add("World");
        stringPriorityQueue.add("Java");
        
        System.out.println("PriorityQueue : " + stringPriorityQueue);
        
        String element = stringPriorityQueue.peek();
        System.out.println("Accessed Element : " + element);
    }
}
```

- 내부 순회하기

```java
import java.util.*;

public class PriorityQueueSample4 {
    public static void main(String[] args) {
        PriorityQueue<String> stringPriorityQueue = new PriorityQueue<>();
        
        stringPriorityQueue.add("Hello");
        stringPriorityQueue.add("World");
        stringPriorityQueue.add("Java");
        
        Iterator iterator = stringPriorityQueue.iterator();
        
        while (iterator.hasNext()) {
            System.out.print(iterator.next() + "\t");
        }
    }
}
```

> PriorityQueue가 순서대로 출력된다고 했는데 주의해야하는 점이 있다. 들어가면서 순서가 정리되면서 들어가는 것이 아니라 head부분만 정리가 되는건지 이해가 잘 가지 않는다.
> 
> 아래는 내가 해당 결과값을 확인해보기 위해 작성한 코드인데 원하는 값으로 나오지 않는다. 해당 부분은 좀 찾아보고 추가적으로 더 적겠다.  
> ~~거지같넹;;;~~

```java
import java.util.Iterator;
import java.util.PriorityQueue;

public class PriorityQueueSample {
    public static void main(String[] args) {
        PriorityQueue<String> stringPriorityQueue = new PriorityQueue<>();

        stringPriorityQueue.add("j");
        stringPriorityQueue.add("i");
        stringPriorityQueue.add("h");
        stringPriorityQueue.add("g");
        stringPriorityQueue.add("f");
        stringPriorityQueue.add("e");
        stringPriorityQueue.add("d");
        stringPriorityQueue.add("c");
        stringPriorityQueue.add("b");
        stringPriorityQueue.add("a");

        System.out.println("stringPriorityQueue.size() : " + stringPriorityQueue.size());
        // 10
      
        System.out.println("그냥 stringPriorityQueue 출력 시 : " + stringPriorityQueue);
        // a, b, e, d, c, i, f, j, g, h

        System.out.print("하나씩 peek()로 출력 시 : ");
        for (String s : stringPriorityQueue) {
            System.out.print(s + "\t");
        }
        System.out.println();
        // a, b, e, d, c, i, f, j, g, h
      
        System.out.print("Iterator로 출력 시 : ");
        Iterator iterator = stringPriorityQueue.iterator();
        while (iterator.hasNext()) {
            System.out.print(iterator.next() + "\t");
        }
        System.out.println();
        // a, b, e, d, c, i, f, j, g, h

        System.out.print("poll로 출력 시 : ");
        while (!stringPriorityQueue.isEmpty()) {
            System.out.print(stringPriorityQueue.poll() + "\t");
        }
        System.out.println();
        // a, b, c, d, e, f, g, h, i, j 

        System.out.println("stringPriorityQueue.size() : " + stringPriorityQueue.size());
    }
}
```

풀린 문제점 :

- toString으로도 출력 시에는 unsorted으로 출력됨.
- Iterator는 순서 상관없이 return 한다고 함([Link for Iterator](https://docs.oracle.com/javase/6/docs/api/java/util/PriorityQueue.html#iterator%28%29)). 순서대로 출력하고자 한다면 `Arrays.sort(pq.toArray())`를 사용할 것
- 또한 들어갈 때마다 모든 요소를 비교해서 순서대로 저장하는 것이 아니다. 어떤 알고리즘으로 저장되는 순서를 알고싶다면 siftUpComparable를 확인해보자

> PriorityQueue를 한번 보고 쓰기에는 좀 어려운 점이 많아보인다.
> 실제로 stackoverflow나 각종 해외 사이트를 보면 대부분의 사람들이 필자와 같은 생각으로 toString이나 iterator로 출력을 했다가 순서대로 출력이 되지 않는다는 질문을 하는 것을 많이 볼 수 있다.
> 
> 또한 초심자가 PriorityQueue를 primitive 타입(;natural ordering) 외 reference 타입으로 할려면 comparator 또는 comparable도 사용을 해야하는데 이 점은 어려워보인다.
> 후에 공부하면서 필요하다고 느낄 때 자세히 살펴보는 것을 추천한다. PriorityQueue 외에도 queue 종류가 너무 많다.....

### References

- [https://www.geeksforgeeks.org/priority-queue-class-in-java/](https://www.geeksforgeeks.org/priority-queue-class-in-java/)
- [https://docs.oracle.com/cd/E17802_01/j2se/j2se/1.5.0/jcp/beta1/apidiffs/java/util/PriorityQueue.html](https://docs.oracle.com/cd/E17802_01/j2se/j2se/1.5.0/jcp/beta1/apidiffs/java/util/PriorityQueue.html)
- [https://stackoverflow.com/questions/13346551/sorting-priorityqueue](https://stackoverflow.com/questions/13346551/sorting-priorityqueue)
- [https://stackoverflow.com/questions/25569625/sorting-priority-queue-in-java](https://stackoverflow.com/questions/25569625/sorting-priority-queue-in-java)
- [https://stackoverflow.com/questions/14397674/java-sorting-a-queue](https://stackoverflow.com/questions/14397674/java-sorting-a-queue)
- [https://github.com/aditya-sridhar/java-priority-queue-example](https://github.com/aditya-sridhar/java-priority-queue-example)
---
title: "스택"
excerpt: "Stack"

categories:
- Data-Structure

tags:
- data structure
- data
- structure
- dynamic
- stack
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

오늘은 긴말 안하고 바로 스택에 대해서 알아보자

### 스택
스택은 실행 시 특정 순서를 따르는 선형 자료 구조이다. 순서는 LIFO(Last In First Out) 또는 FILO(First In Last Out)일 수도 있다.

다음은 스택에서 사용되는 기본적인 수행 용어이다.
- Push : 스택에 요소 하나를 더한다. 만약 스택이 가득 찼다면 오버플로우(Overflow) 상태라고 뜰 것이다. &#42;자바에서는 느낌이 조금 다를지도?...
- Pop : 스택에서 요소 하나를 제거한다. 요소들은 들어간 순서의 반대로 나온다. 만약 스택이 비어있다면 언더플로우(Underflow) 상태라고 뜰 것이다. &#42;자바에서는 `EmptyStackException`으로 뜬다.
- Peek or Top : 스택에 가장 마지막에 push한 요소를 리턴한다. &#42;자바에서는 `peek`. `top`은 없다.
- isEmpty : 스택이 비어있다면 `true`를 반환하고 아니라면 `false`를 반환한다.

### 스택에 대해 이해하기
현실에서도 많은 것들을 스택의 예로 들 수 있다. 음식점이나 집에 쌓여있는 접시를 생각해보자. 접시를 꺼낼때(물론 어떻게든 가운데 접시를 꺼낼 수도 있지만 대다수가) 가장 위에 있는 접시부터 꺼낼 것이다. 이것도 LIFO/FILO 순서를 따른다고 볼 수 있다.

#### 스택 구현 방법
스택은 배열(array) 또는 연결 리스트(Linked List)를 사용해서 구현할 수 있다.

###### 배열을 이용한 스택 구현
```java
public class StackArray {
    static final int MAX = 1000;
    int top;
    int a[] = new int[MAX];  // Maximum size of Stack

    boolean isEmpty() {  // top이 0보다 작다면 아무것도 없음으로 true 리턴
        return (top < 0);
    }
    
    StackArray() {  // 항상 top = -1로만 생성할 수 있는 생성자
        top = -1;
    }
    
    boolean push(int x) {
        if (top >= (MAX - 1)) {  // top이 MAX-1 값보다 크면 용량 초과
            System.out.println("Stack Overflow");
            return false;
        } else {
            a[++top] = x;  // top의 숫자 증가 및 배열[++top] 인덱스에 값 넣기
            System.out.println(x + " pushed into stack");
            return true;
        }
    }
    
    int pop() {
        if (top < 0) {  // 아무런 값도 없을 시 Underflow
            System.out.println("Stack Underflow");
            return 0;
        } else {
            int x = a[top--];  // 값 하나를 뺌으로 top--, peek는 --없이
            return x;
        }
    }
    
    // 위와 동일 a배열의 인덱스에 top--만 다름
    int peek() {
        if (top < 0) {
            System.out.println("Stack Underflow");
            return 0;
        } else {
            int x = a[top];
            return x;
        }
    }
    
    void print() {
        for (int i=top; i>-1; i--) {
            System.out.print(a[i] + "\t");
        }
    }
}

public class Main {
    public static void main(String[] args) {
        StackArray s = new StackArray();
        s.push(10);
        s.push(20);
        s.push(30);
        System.out.println(s.pop() + " Popped from stack");
        System.out.println("Top element is : " + s.peek());
        System.out.print("Elements present in stack : ");
        s.print();
    }
}
```
장점 : 쉽게 구현할 수 있다. 메모리 관련도 있지만 c언어쪽이기에 언급은 안하겠다.  
단점 : 동적이지 않다. 런타임에 따라서 크기가 유동적이지 못하다.

###### 연결 리스트를 이용한 스택 구현
```java
public class StackLinkedList {
    
    StackNode root;  // 노드의 최초 시작점이자 삽입시 top부분
    
    static class StackNode {
        int data;
        StackNode next;  // 다음 노드 주소
        
        StackNode(int data) {  // data가 들어와야지만 생성
            this.data = data;
        }
    }
    
    public boolean isEmpty() {  // 노드 최초 시작점이 null이라면 true 반환
        if (root == null) return true;
        else return false;
    }
    
    public void push(int data) {
        StackNode newNode = new StackNode(data);  // 일단 노드 객체 생성
        
        if (root == null) root = newNode;  // 최초 노드가 없다면 최초에 대입
        else {
            StackNode tmp = root;  // 임시 tmp에 root를 넣고
            root = newNode;  // root에 새로 push한 노드 삽입
            newNode.next = tmp;  // 그후 push한 노드의 다음으로 tmp(이전 root) 대입
        }
        System.out.println(data + " pushed to stack");
    }
    
    public int pop() {
        int popped = Integer.MIN_VALUE;  // -21_4748_3648 : -21억 4748만까지 갈 일이 있나? c언어쪽에선 뭐가 다른가?
        if (root == null) System.out.println("Stack is Empty");  // 최초 노드가 없을 시 비어있다고 출력
        else {
            popped = root.data;
            root = root.next;
        }
        return popped;
    }
    
    public int peek() {
        if (root == null) {
            System.out.println("Stack is Empty");
            return Integer.MIN_VALUE;
        } else return root.data;
    }

    public static void main(String[] args) {
        StackLinkedList sll = new StackLinkedList();
        
        sll.push(10);
        sll.push(20);
        sll.push(30);
        System.out.println(sll.pop() + " popped from stack");
        System.out.println("Top element is " + sll.peek());
    }
    
}
```
장점 : 연결 리스트로 구현 시 런타임에 따라서 스택의 크기가 유동적으로 변할 수 있다.  
단점 : 포인터 할당으로 인해 추가적인 메모리가 필요하다(java에서는 객체 주소를 말하는 것?).

### 자바에서의 스택 클래스(Stack Class in Java)
자바 콜렉션 프레임워크에서는 이전에 설명한 스택 모델과 동일한 개념의 스택 클래스를 제공합니다. 클래스는 LIFO를 기반으로 설계되어있습니다.  
`Push`와 `Pop` 말고도 `empty`, `search` 그리고 `peek`라는 3개의 기능을 더 제공합니다.  
스택 클래스는 Vector 클래스를 상속 받기에 Vector 클래스의 메서드도 사용이 가능하다.

![스택 클래스의 상속 관계](/assets/images/2022/hierarchy-of-the-Stack-class.png)
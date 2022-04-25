---
title: "트리"
excerpt: "Tree"

categories:
- Data-Structure

tags:
- data structure
- data
- structure
- non linear
- binary
- tree
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


## 트리(Tree)

`Arrays`, `Linked List`, `Stack`  그리고 `Queue`와는 달리 `tree`는 계층적 자료 구조 성질을 지니고 있다.   

트리 용어로는 `parent`와 `child` 또는 `Children`이 있다. 아래의 그림에서 a는 f의 자식이고 f는 a의 부모이다.

![binary-tree-example](/assets/images/2022/binary-tree-example.JPG)

### 트리 사용 이유

1. 정보를 계층적으로 저장하고 싶을 때 사용된다. 예를 들면 컴퓨터의 폴더에 저장하는 것과도 같다고 생각할 수 있다.
2. 트리는 중간의 속도로 엑세스 또는 찾기가 가능하다(Linked List보다는 빠르고 Array보다는 느리다).
3. 삽입과 삭제도 중간의 속도로 한다(Array보다는 빠르고 Unordered Linked List보다는 느리다).
4. Array와는 다르고 Linked List와 같이 트리는 노드끼리 pointer로 연결되어있다.

### 트리의 특징

1. 계층적 데이터를 다룰 수 있다.
2. 정보를 쉽게 찾을 수 있게 한다(traversal 참고).
3. 정렬된 데이터 리스트를 다룰 수 있다.
4. 작업 흐름도를 시각적으로 처리할 수 있다.
5. 라우팅 알고리즘
6. 다단계 의사결정이 가능하다(business chess 참고).

**Binary Tree** : 2개의 자식으로만 나뉘는 트리를 이진 트리(Binary Tree)라고 구분한다. 이진 트리의 각 엘레멘트마다 자식을 2개만 갖을 수 있기에 왼쪽과 오른쪽 자식으로 칭한다.

트리의 노드는 아래 구성을 포함한다.
1. 데이터
2. 왼쪽 자식을 향한 포인터
3. 오른쪽 자식을 향한 포인터

###### 이진 트리 구현

```java
class Node {
    int key;
    Node left, right;
    
    public Node(int item) {
        key = item;
        left = right = null;
    }
}
```

###### 이진 트리 활용

```java
class Node {
    int key;
    Node left, right;
    
    public Node(int item) {
        key = item;
        left = right = null;
    }
}

class BinaryTree {
    // Root of Binary Tree
    Node root;
    
    // 생성자
    BinaryTree(int key) {
        root = new Node(key);
    }
    
    BinaryTree() {
        root = null;
    }
    
    public static void main(String[] args) {
        BinaryTree tree = new BinaryTree();
        
        // root 트리 생성
        tree.root = new Node(1);
        /* 아래와 같음
            1
          /   \
        null  null          */
        
        tree.root.left = new Node(2);
        tree.root.right = new Node(3);
        /* 아래와 같음
             1
         /       \
       2           3
     /   \       /   \
   null  null  null  null   */
        
        tree.root.left.left = new Node(4);
        /* 아래와 같음
             1
         /       \
       2           3
     /   \       /   \
    4    null  null  null
  /  \
null  null                  */
    }
}
```

###### 요약

트리는 계층적 자료 구조이다.  
트리의 핵심 사용 이유는 데이터를 계층적 저장하고 보통의 속도로 엑세스/찾기/삽입/삭제를 해야할 때이다.  
이진 트리는 트리 중에서 특이한 케이스이며 어떤 노드도 자식이 2개 있는 것이다.

> 자바에 있는 TreeSet 구현체에 대해서 공부를 할까하다가 비전공자다보니 기본적인 트리라는 것에 대해서 공부하고 들어가는 것이 더 좋을 듯 하여 트리에 대해서 먼저 알아보았다.
> 
> 자바의 TreeSet에 대해 들어가기 전에 이진 트리에 어떤 타입이 있는지에 대해서 글을 하나 더 적고 들어가겠다.

### References

- [https://www.geeksforgeeks.org/binary-tree-set-1-introduction/](https://www.geeksforgeeks.org/binary-tree-set-1-introduction/)
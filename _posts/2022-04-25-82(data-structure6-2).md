---
title: "자바의 트리세트"
excerpt: "TreeSet"

categories:
- Data-Structure

tags:
- data structure
- data
- structure
- non linear
- TreeSet
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


## 트리 세트(TreeSet)

`TreeSet`은 아래의 그림과 같이 `SortedSet`과 `NavigableSet` 인터페이스의 구현체 클래스 중 하나이다.

`Set`의 성질과 동일하게 동일한 데이터는 집어넣을 수 없다.
하지만 순서는 natural ordering(오름차순)을 지키며 Comparator를 통해서 지정할 수 있다.  
간혹 set의 성질 중 하나인 순서를 지키지 않는다고 적으신 분들이 계신데 해외 사이트 몇군데 또는 TreeSet 클래스에서 생성자 부분을 살펴보면 `sorted according to the natural ordering`이라고 적혀있다.
그냥 순서를 안지키는 것이 아니니 일반적인 `HashSet`을 썼을 때처럼 무작위로 출력되는 것이 아니다.


![hierarchy-of-the-TreeSet](/assets/images/2022/hierarchy-of-the-TreeSet.JPG)


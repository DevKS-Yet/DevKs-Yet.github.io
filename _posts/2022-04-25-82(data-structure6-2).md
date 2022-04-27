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

위 사진을 보면 TreeSet은 NavigableSet -> SortedSet -> Set을 상속 받는 것을 알 수 있다.
순서 정렬이 가능한 Set가 딱봐도 보이니 추가적인 설명은 안하겠다.
~~사실 나도 잘 모른다... 누가 잘 적어서 설명 '해줘'~~

#### TreeSet은 내부적으로 어떻게 작동되는가?

TreeSet은 자가 균형 이진 탐색 트리(예: 레드-블랙 트리)를 기본적으로 구현하고 있다.
그렇기에 add, remove 그리고 search 같은 수행 작업은 O(log(N)) 시간이 걸린다. ~~참고로 나도 수학과지만 저게 뭔 시간인지 모른다 묻지마라~~

추가적인 것은 따로 알아보고 일단 어떻게 선언하고 사용하는지 알아보자

#### TreeSet 생성하기

###### 기본 생성자로 생성하기

이 생성자는 요소를 저장할 때 기본적인 natural sorting order로 들어간다.

```java
TreeSet ts = new TreeSet();
```

###### 정의한 정렬로 생성하기

이 생성자는 요소를 저장할 때 외부에서 정의한 순서대로 정렬한다.

```java
TreeSet ts = new TreeSet(Comparator comp);
```

###### 콜렉션으로 생성하기

이 생성자는 정의된 콜렉션 요소가 저장되며 기본적인 natural sorting order로 저장된다. 저장되는 모든 요소를 `Comparable` 인터페이스를 구현해야한다.

```java
TreeSet ts = new TreeSet(Collection col);
```

###### SortedSet으로 생성하기

이 생성자는 `SortedSet`에 있는 모든 요소를  natural sorting order로 TreeSet에 저장한다.
사용하는 경우는 SortedSet과 TreeSet의 정렬 순서를 다르게 하고 싶어할 때 사용한다.

```java
TreeSet ts = new TreeSet(SortedSet s);
```
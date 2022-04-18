---
title: "연결 리스트"
excerpt: "Linked-List"

categories:
- Data-Structure

tags:
- data structure
- data
- structure
- dynamic
- linked list
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

저번에 배열에 대해서 알아보았는데 이제는 선형 자료 구조 중 동적인 연결 리스트에 대해서 알아보자

배열과 동일하게 연결 리스트도 선형 자료 구조이다. 다만 배열과 다른 점은 연결 리스트의 각 데이터는 연속된 주소에 저장되는 것이 아니다.  
각 엘레멘드가 포인터를 사용하여 연결되어 있는 것이다.

### 연결 리스트 사용 이유
동일한 타입의 데이터는 배열을 통해서도 저장할 수 있지만 배열은 아래와 같이 몇가지의 제한사항이 있다.
1. 배열의 크기는 고정임으로 배열 생성시 제한을 어디에 둘지 알아야한다. 또한 제한을 둔 곳까지 사용하지 않더라도 메모리에는 할당이 되어있다.
2. 배열에 요소를 삽입하는데 많은 비용이 들 수 있다.  
예를 들면 `id[] = [1000, 1010, 1050, 2000, 2040]`이 있고 오름차순을 지키며 새로운 ID로 1005를 삽입하고자 한다면 1000을 제외한 나머지를 옮겨야한다.  
삭제 또한 마찬가지이다.

### 배열과 비교했을때 장점
1. 동적 사이즈
2. 쉬운 삽입 및 삭제


### 단점
1. 랜덤 엑세스가 불가함. 첫 번째 노드부터 접근할 수 있음. 그르므로 바이너리 서치에는 연결 리스트를 사용하는 것이 효율적이지 않음
2. 각 요소에 추가적으로 포인터를 위한 추가 메모리 공간이 필요함.
3. 캐시 친화적이지 않음. 배열의 요소들은 연속적인 위치임으로 '참조 지역성의 원리(Locality of reference)'이지만 연결 리스트는 그렇지 않음

#### Linked List 생성
```java
import java.util.Arrays;
import java.util.LinkedList;

public class LinkedListSample1 {
    public static void main(String[] args) {
        LinkedList<Integer> integerLinkedList1 = new LinkedList<Integer>();  // 타입 지정
        LinkedList<Integer> integerLinkedList2 = new LinkedList<>();  // 타입 생략 가능
        LinkedList<Integer> integerLinkedList3 = new LinkedList<>(integerLinkedList1);  // 다른 Collection값으로 초기화
        LinkedList<Integer> integerLinkedList4 = new LinkedList<>(Arrays.asList(1, 2, 3, 4, 5));  // Arrays.asList()로 초기화
    }
}
```
위와 같이 여러가지 방법으로 Linked List를 생성할 수 있다.

#### Linked List 엘레멘트 추가/변경
```java
import java.util.LinkedList;

public class LinkedListSample2 {
    public static void main(String[] args) {
        LinkedList<String> colors = new LinkedList<>();
        // add() method를 이용하여 추가
        colors.add("Black");
        colors.add("White");
        colors.add(0, "Green");  // index : 0에 Green을 추가
        colors.add("Red");

        // set() method
        colors.set(1, "Blue");  // index : 1에 위치한 값을 Blue로 변경

        System.out.println(colors);
    }
}
```
인덱스 없이 요소만 적었을 시에 인덱스 끝에 삽입된다. add() 메서드에서 인덱스를 사용했을 시 해당 인덱스에 추가된 값이 있다면 해당 값은 다음 인덱스로 밀려나도 추가로 적은 값이 해당 인덱스에 들어간다.

#### Linked List 엘레멘트 삭제
```java
import java.util.Arrays;
import java.util.LinkedList;

public class LinkedListSample3 {
    public static void main(String[] args) {
        LinkedList<String> colors = new LinkedList<>(Arrays.asList("Black", "White", "Green", "Red"));
        String removedColor = colors.remove(0);  // 해당 인덱스 값을 제거하고 제거도니 값 리턴
        System.out.println("Removed color is " + removedColor);
        
        colors.remove("White");  // 값이 White와 동일한 것을 삭제
        System.out.println(colors);
        
        colors.clear();  // LinkedList 전체 삭제
        System.out.println(colors);
    }
}
```

#### LinkedList 전체 값 확인
```java
import java.util.Arrays;
import java.util.Iterator;
import java.util.LinkedList;
import java.util.ListIterator;

public class LinkedListSample4 {
    public static void main(String[] args) {
        LinkedList<String> colors = new LinkedList<>(Arrays.asList("Black", "White", "Green", "Red"));
        // for-each loop
        for (String color : colors) {
            System.out.print(color + "\t");
        }
        System.out.println();
        
        // for loop
        for (int i=0; i<colors.size(); ++i) {
            System.out.print(colors.get(i) + "\t");
            System.out.println();
        }
        System.out.println();
        
        // using iterator
        Iterator<String> iterator = colors.iterator();
        while (iterator.hasNext()) {
            System.out.print(iterator.next() + "\t");
        }
        System.out.println();
        
        // using listiterator
        ListIterator<String> listIterator = colors.listIterator(colors.size());
        while (listIterator.hasPrevious()) {
            System.out.print(listIterator.previous() + "\t");
        }
        System.out.println();
    }
}
```

> Linked List는 여기까지만 적고 스택으로 넘어가도록 하겠다.  
> 추후에 이 밖에도 Circular Linked List 또는 Double Linked List에 대해서도 정리하겠다.

### Reference
- [https://www.geeksforgeeks.org/linked-list-set-1-introduction/?ref=lbp](https://www.geeksforgeeks.org/linked-list-set-1-introduction/?ref=lbp)
- [https://www.geeksforgeeks.org/linked-list-set-2-inserting-a-node/?ref=lbp](https://www.geeksforgeeks.org/linked-list-set-2-inserting-a-node/?ref=lbp)
- [https://www.geeksforgeeks.org/linked-list-set-3-deleting-node/?ref=lbp](https://www.geeksforgeeks.org/linked-list-set-3-deleting-node/?ref=lbp)
- [https://www.geeksforgeeks.org/linked-list-vs-array/?ref=lbp](https://www.geeksforgeeks.org/linked-list-vs-array/?ref=lbp)
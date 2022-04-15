---
title: "자료 구조"
excerpt: "Data-Structure"

categories:
- Data-Structure

tags:
- data structure
- data
- structure
---

# 자료 구조
이번에는 백엔드 개발자로서 꼭 알아야하는 부분이라고 생각하는 자료 구조에 대해서 공부를 시작할려고 한다.  
자료 구조를 알아야지 후에 좀 더 효율적으로 컴퓨터를 운용할 수 있기 때문이다.

공부하고자 하는 자료 구조는 아래와 같으며 추후 링크를 따로 걸도록 하겠다.
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

간략하게 선형/비선형, 정적/동적 자료 구조에 대해 설명을 하고자 한다.

## 선형 자료 구조(Linear Data Structures)
선형 자료 구조란 데이터들이 순차적이거나 이전과 이후에 삽입된 데이터끼리 연결된 선형적인 자료 구조를 뜻한다.  
선형은 자료들 간의 앞뒤 관계가 1:1 관계이다.

선형 자료 구조에는 정적과 동적인 것으로 나뉘어져있으며 선형 자료구조 중 정적인 것에는 `Array`가 있고 동적에는 `Linked List, Stack, Queue`가 있다.  
그렇다면 정적과 동적이라는 뜻에 대해 간략하게 알아보자.

#### 정적 자료 구조란?(Static Data Structure)
정적 자료 구조에서는 사이즈가 정해져있으며 내부 데이터는 변경이 가능하나 구조 자체의 사이즈 변경은 불가능 하다.

자바를 배울때 처음으로 배우는 구조가 `Array`일텐데 잘 기억을 떠올려보면 불편했던 점이 한두가지가 아니다.  
필자만 해도 흔히 했던 학생성적 프로그램에서 `String[]`을 사용하였는데 사이즈가 지정이 되어있으니 더 추가하고 싶거나 삭제했을 경우에도 다시 그 자리에 넣기가 매우 힘들었다.  
처음에 지정한 사이즈보다 초과가 될 시에는 사이즈를 추가한 배열을 새로 생성하고 거기에 자료를 집어넣었으나 지금보면 얼마나 불필요한 작업인가 싶다.  
이렇듯 정적 자료 구조란 사이즈가 유동적이지 못하고 고정되어있는 것을 뜻한다.

#### 동적 자료 구조란?(Dynamic Data Structure)
동적 자료 구조는 정적과 다르게 사이즈가 정해져있지않고 연산 또는 작업중에 사이즈 변경이 가능한 것들이다.  
동적 자료 구조은 실시간으로 자주 변경되는 것에 유연하게 반응할 수 있도록 설계되어있다.

###### 정적 자료 구조 vs 동적 자료구조
정적 자료 구조는 사이즈가 정해져있지만 동적 자료 주고는 런타임 도중에도 사이즈를 변경할 수 있다.  
동적 자료 구조를 사용하면 정적 자료 구조보다 효율적인 메모리 사용(정말 효율적으로 사용하고자 한다면 정적 자료 구조)와 코드 최소화(이건 진짜다)를 시킬 수 있다.

그렇다면 정적 자료 구조 쓸일이 없지 않는가 라는 생각이 들 수 있다.  
전혀 그렇지 않다.  
Competitive Programming과 같이 제한이 주어지는 경우에는 메모리 사용량을 최소화 시키고 정해진 범위 내에서만 시행을 시켜야하기에 정적 자료 구조가 사용하기에는 더 편할 수 있다.  
무한 반복 같지만 그렇다고 해서 동적 자료 구조를 아예 안쓰는 것도 아니다.

그러니 너무 복잡하게 생각하지 않고 일단 자료 구조에 대해서 공부한 뒤에 하나씩 사용을 해보면서 장단점을 정리해보고 상황은 매우 다양하기 자기가 직접 생각하여 알맞는 자료 구조를 사용할 수 있도록 해보자

## 비선형 자료 구조(Non-Linear Data Structure)
말장난 같이 느낄 수 있지만 데이터가 순차적이지 않거나 선형이지 않은 자료 구조를 비선형 자료 구조라 한다.  
비선형은 자료들 간의 앞뒤 관계가 1:n, 또는 n:n의 관계가 되며 계층적 구조를 나타내기에 적합하다.


### 차이점에 대한 정리

###### 선형 / 비선형 자료 구조

| Linear Data Structure            | Non-linear Data Structure       |
|:---------------------------------|:--------------------------------|
| 데이터가 순차적이며 서로서로 전 후 데이터끼리 연결되어있음 | 데이터들이 계층적(hierarchically)으로 연결됨 |
| single level로 형성                 | multiple level로 형성              |
| 비선형에 비해 구현이 쉬움                   | 선형에 비해 구현이 복잡함                  |
| 한번만 실행해도 모든 데이터를 횡단 가능           | 한번만에 모든 데이터 횡단 불가능              |
| 사이즈가 고정임으로 지속적인 메모리 추적이 필요함      | 사이즈가 유동적임으로 지속적인 메모리 추적이 불필요함 |

###### 정적 / 동적 자료 구조

| Static Data Structure     | Dynamic Data Structure |
|:--------------------------|:-----------------------|
| 자료 구조 사이즈가 고정적임           | 자료 구조 사이즈가 유동적임        |
| 사이즈가 고정이기에 극한의 메모리 최적화 가능 | 극한으로 메모리를 최적화 할 수는 없지만 유동적으로 사이즈 변경이 가능하여 용이함 |
| 프로그램을 구현할 때 정적 자료 구조의 메모리를 keep track해야함 | 프로그램을 구현할 때 사이즈에 대해서 체크할 필요까지는 없음 |

&#42;참고로 C언어에서는 정적 자료 구조는 메모리 주소 할당이 유동적이고 동적 자료 구조는 메모리 주소 할당이 고정이라고 하지만 Java는 static을 제외한 모든 객체는 heap에 유동적으로 주소가 저장된다.  
윗 줄에 관해서는 `call by reference, call by value`에 대해 알면 좋다. 아직 다루지는 않을 것이지만 궁금하신 분은 링크를 참고하자([혼잣말하는 개발자 call by reference/value](https://dev-cool.tistory.com/21 "ang SiwonDdi")).


> 추가적으로 여기에 적지는 않았지만 `Hash Tables`도 있다. 이것은 선형과 비선형의 특징을 둘다 띄고 있다.  
> Hash Tables에 대해서도 다루긴 하겠지만 선형과 비선형 자료 구조를 끝낸 후에 다루겠다.
> 
> 앞으로는 선형 자료 구조의 정적 자료 구조부터 시작하여 동적 그리고 비선형 자료 구조에 대해서 알아보겠다.

### Reference
- [https://www.geeksforgeeks.org/data-structures](https://www.geeksforgeeks.org/data-structures)
- [https://www.geeksforgeeks.org/static-data-structure-vs-dynamic-data-structure](https://www.geeksforgeeks.org/static-data-structure-vs-dynamic-data-structure)
- [https://codinghero.ai/static-and-dynamic-data-structures-explained-to-kids](https://codinghero.ai/static-and-dynamic-data-structures-explained-to-kids)
- [https://dev-cool.tistory.com/21](https://dev-cool.tistory.com/21)
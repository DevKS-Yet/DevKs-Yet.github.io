---
title: "자바의 정석 9일차"
excerpt: "post"

categories:
- standard-of-java
tags:
- java
- book
---

# Chapter 04 조건문과 반복문(if, switch, for, while statement)

## 2.반복문 - for, while, do-while
반복문이란 어떤 작업을 반복적으로 수행되도록 할 때 사용된다.  
for문이나 while문에 속한 문장은 조건에 따라 한 번도 수행되지 않을 수 있지만 do-while문에 속한 문장은 무조건 최소한 한 번은 수행될 것이 보장된다.

### 2.1 for문
for문은 반복 횟수를 알고 있을 때 적합하다.

```java
for (초기화; 조건식; 증감식) {
    // 수행될 문장
}
```
for문은 위와 같은 구조로 이루어져있다.

###### 초기화
대부분의 for문은 초기화 변수를 하나만 사용하지만 추가적으로 변수를 더하여 사용할 수 있다.

```java
for (int i=1; i<=10; i++) { ... }
for (int i=1, j=0; i<=10; i++) { ... }
```

###### 조건식
중앙에 들어가는 조건식의 값이 참이면 반복을 계속하고 거짓을 하면 반복 중단 및 for문을 벗어난다.

```java
for (int i=1; i<=10; i++) { ... }
```

###### 증감식
반복문을 제어하는 변수의 값을 증가 또는 감소시키는 식이다. 주로 ++, --를 사용하지만 +=, -=, *=, /=, %=도 사용이 가능하다.  
또한 증감식도 ','를 이용해서 두 문장 이상을 하나로 연결해서 쓸 수 있다.

```java
for (int i=1, j=10; i<=10; i++, j--) { ... }
```

##### 예제 4-12/ch4/FlowEx12.java
```java
class FlowEx12 {
    public static void main(String[] args) {
        for (int i=1; i<=5; i++) {
            System.out.println(i);
        }
        for (int i=1; i<=5; i++) {
            System.out.print(i);
        }
        System.out.println();
    }
}
```
위 예제를 통해서 초기화 변수가 1부터 시작하여 5까지만 반복하는 것을 확인할 수 있다.

##### 예제 4-13/ch4/FlowEx13.java
```java
class FlowEx13 {
    public static void main(String[] args) {
        int sum = 0;
        for (int i=1; i<=10; i++) {
            sum += i;
            System.out.printf("1부터 %2d 까지의 합: %2d%n", i, sum);
        }
    }
}
```

##### 예제 4-14/ch4/FlowEx14.java
```java
class FlowEx14 {
    public static void main(String[] args) {
        for(int i=1, j=10; i<=10; i++, j--) {
            System.out.printf("%d \t %d%n", i, j);
        }
    }
}
```


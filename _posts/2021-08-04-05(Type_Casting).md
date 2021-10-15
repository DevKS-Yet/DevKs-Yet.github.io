---
title: "05&#46; 형 변환"
excerpt: "기본 자바"

categories:
  - 자바(기본)
tags:
  - 자바
  - java
  - basic
  - type
  - casting
  - 형
  - 변환
---

## 형 변환(Type Casting)
- 형 변환은 어떤 하나의 원시 자료형의 값을 다른 형의 값으로 바꿀 때 사용 됩니다.
- 두 개의 형 변환이 있습니다.
  - Widening Casting(자동) - 작은 타입을 큰 타입으로 자동적으로 바꿔줍니다.  
  byte -> short -> char -> int -> long -> float -> double
  - Narrowing Casting(수동) - 큰 타입을 작은 타입은 수동적으로 바꿔줘야합니다.  
  double -> float -> long -> int -> char -> short -> byte

## Widening Casting(작은 것에서 큰 걸로)
- Widening Casting은 작은 타입에서 큰 타입으로 변환할때 자동적으로 실행 됩니다.
```java
public class Main {
  public static void main(String[] args) {
    int myInt = 9;
    double myDouble = myInt; // 자동적으로 int를 double로 형 변환 해줍니다.

    System.out.println(myInt); // 출력: 9
    System.out.println(myDouble); // 출력: 9.0
  }
}
```

## Narrowing Casting
- Narrowing Casting은 꼭 수동적으로 값 앞에 변환하고자 하는 형을 적어줘야합니다.
```java
public class Main {
  public static void main(String[] args) {
    double myDouble = 9.78d; // 여기서 d는 double형이기에 붙였지만 안붙여도 괜찮습니다.
    int myInt = (int) myDouble; // 수동 변환: double에서 int로

    System.out.println(myDouble); // 출력: 9.78
    System.out.println(myInt); // 출력: 9 (int형은 정수만 취급하기에 뒤에 소수점은 사라집니다.)
  }
}
```

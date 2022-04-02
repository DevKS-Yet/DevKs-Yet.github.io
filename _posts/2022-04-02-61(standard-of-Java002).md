---
title: "자바의 정석 2일차"
excerpt: "post"

categories:
- standard-of-java
tags:
- java
- book
---

# Chapter 02 변수(Variable)

## 변수(Variable)
결국에 프로그래밍이라는 것은 데이터를 잘 다뤄야하는 것이다. 그렇기 위해서는 변수에 대해서 알아본다.

### 1.1 변수(variable)란?
수학에서는 '변수'란 '변하는 수'로 정의하지만 프로그래밍 언어에서는 값을 저장할 수 있는 메모리상의 공간을 의미한다(수학과라서 이 책을 읽기 전까지 변하는 수로 알고있었다). 물론 이 공간에 저장된 값이 변경이 불가능하지는 않다. 변경 될 수 있기에 변수라는 이름이 붙여진 것이다.

### 1.2 변수의 선언과 초기화
**"변수 초기화란, 변수를 사용하지 전에 처음으로 값을 저장하는 것"**
- 선언방법
```java
int age;  // age라는 이름의 변수를 선언
```
`int`는 각종 변수 타입으로 변경 가능하며 변수의 이름은 예약어를 제외하고 사용자 마음대로 만들 수 있다.
- 변수의 초기화
```java
int a;  // a, b라는 변수는 초기화가 안된 상태. 전역변수일 경우에는 컴파일 도중 알아서 int의 기본값인 0을 대입
int b;
int x = 0;  // x, y라는 변수에 0으로 초기화
int y = 0;
 ```
  변수의 종류에 따라서 변수의 초기화를 생략할 수 있는 경우도 있지만 적절한 값으로 항상 초기화 하는 것이 좋다.

##### 예제 2-1/ch2/VarEx1.java
변수 초기화
```java
class VarEx1 {
    public static void main (String[] args) {
        int year = 0;
        int age = 14;
      System.out.println(year);
      System.out.println(age);
        
        year = age + 2000;
        age = age + 1;
      System.out.println(year);
      System.out.println(age);
    }
}
```

##### 예제 2-2/ch2/VarEx2.java
두 변수의 값 교환하기
```java
class VarEx2 {
    public static void main(String[] args) {
        int x = 10, y = 20;  // 동일한 타입의 변수는 생략해서 이렇게 적을 수도 있다.
        int tmp = 0;

      System.out.println("x: " + x + "\ny: " + y);
      
        tmp = x;
        x = y;
        y = tmp;

      System.out.println("x: " + x + "\ny: " + y);
    }
}
```
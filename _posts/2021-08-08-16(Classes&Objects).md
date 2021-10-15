---
title: "16&#46; Classes and Objects"
excerpt: "기본 자바"

categories:
  - 자바(기본)
tags:
  - 자바
  - java
  - basic
  - classes
  - objects
  - 클래스
  - 객체
---

## 클래스와 객체(Classes/Objects)
- 전에도 말한 것과 같이 자바는 객체지향 프로그래밍 언어입니다.
- 자바는 클래스와 객체와 관련되어있으며 그 안에는 속성과 메서드도 있습니다. 예를 들면, 현실에서 '자동차' 라는 객체가 있고 자동차에는 무게, 색상 같은 속성이 있으며 전진, 후진, 브레이크 같은 메서드가 있습니다.
- 클래스는 객체 설계도 또는 객체 생성을 위한 블루프린트 라고 생각하시면 좋습니다.

## 클래스 생성(Create a Class)
- 클래스 생성을 위한 키워드는 `class`입니다.
```java
public class '클래스명' {
  // 속성 또는 메서드를 넣는 공간
}
```
  - 클래스의 명의 첫 문자는 항상 대문자로 합니다.

## 객체 생성(Create an Object)
- 객체 생성을 위한 키워드는 `new 클래스명()`입니다.
```java
클래스명 변수명 = new 클래스명();
```
  - 소괄호는 매개변수를 위한 것인데 매개변수에 관해서는 메서드와 생성자에 대해서 포스팅할때 자세히 설명하겠습니다.


- 위와 같은 방법으로 클래스명을 Main이라고 한 클래스를 만들었을때 Main의 객체를 생성해보겠습니다.
```java
public class Main {
  int x = 5;

  public static void main(String[] args) {
    Main obj = new Main();
    System.out.println(obj.x);
  }
}
```

## 다중 객체(Multiple Objects)
- 하나의 클래스를 통해서 여러 개의 객체를 생성할 수 있습니다.
```java
public class Main {
  int x = 5;

  public static void main(String[] args) {
    Main obj1 = new Main(); // 객체1
    Main obj2 = new Main(); // 객체2
    System.out.println(obj1.x);
    System.out.println(obj2.x);
  }
}
```

## 여러 클래스 사용(Using Multiple Classes)
- 다른 클래스 파일에서 다른 클래스의 객체를 생성할 수도 있습니다. 이것을 통해 클래스를 좀 더 보기 쉽게 정리 할 수 있습니다(하나의 클래스에는 속성값만, 다른 하나는 메서드만).
```java
public class Main {
  int x = 5;
}
```
```java
class Second {
  public static void main(String[] args) {
    Main obj = new Main();
    System.out.println(obj.x); // 출력: 5
  }
}
```

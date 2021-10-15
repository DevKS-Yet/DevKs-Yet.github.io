---
title: "17&#46; Classes Attributes"
excerpt: "기본 자바"

categories:
  - 자바(기본)
tags:
  - 자바
  - java
  - basic
  - classes
  - attributes
  - 클래스
  - 속성
---

## 클래스 속성(Class Attributes)
- 이전 포스트에서 Main 클래스 안에 int x라는 것이 있었는데 그것이 클래스의 속성입니다.
```java
public class Main {
  int x = 5;
}
```
  - 클래스 속성의 다른 이름은 '필드'라고 합니다.

## 속성 접근(Accessing Attributes)
- 속성값에 접근하기 위해서는 먼저 클래스의 객체를 생성하고 점(`.`)을 사용하면 됩니다.
```java
public class Main {
  int x = 5;

  public static void main(String[] args) {
    Main obj = new Main();
    System.out.println(obj.x);
  }
}
```

## 속성 변경(Modify Attributes)
- 속성 접근과 같은 방법을 통해 변경 또한 할 수 있습니다.
```java
public class Main {
  int x;

  public static void main(String[] args) {
    Main obj = new Main();
    obj.x = 40;
    System.out.println(obj.x);
  }
}
```

- 이미 값이 있는 속성을 덮어씌우기(Override)
```java
public class Main {
  int x = 10;

  public static void main(String[] args) {
    Main obj = new Main();
    obj.x = 25;
    System.out.println(obj.x); // 출력: 25
  }
}
```

## 다중 객체(Multiple Objects)
- 하나의 클래스를 통해 여러 개의 객체를 생성할 수 있으며 이때 하나의 객체만의 속성 값을 변경할 수도 있습니다.
```java
public class Main {
  int x = 5;

  public static void main(String[] args) {
    Main obj1 = new Main();
    Main obj2 = new Main();
    obj2.x = 25;
    System.out.println(obj1); // 출력: 5
    System.out.println(obj2); // 출력: 25
  }
}
```

## 다중 속성(Multiple Attributes)
- 원하는 만큼의 속성을 부여할 수 있습니다.
```java
public class Main {
  String fname = "KyuSang";
  String lname = "Cho"

  public static void main(String[] args) {
    Main obj = new Main();
    System.out.println("Name : " + obj.fname + " " + obj.lname);
  }
}
```

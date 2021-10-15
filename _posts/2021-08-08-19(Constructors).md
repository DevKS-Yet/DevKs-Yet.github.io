---
title: "19&#46; Constructors"
excerpt: "기본 자바"

categories:
  - 자바(기본)
tags:
  - 자바
  - java
  - basic
  - constructors
  - 생성자
---

## 생성자(Constructor)
- 생성자는 객체 초기화를 위해서 사용되는 특별한 메서드입니다. 생성자는 객체가 생성될 때 호출이 됩니다. 생성자를 통해서 객체 생성과 동시에 속성 값을 지정할 수 있습니다.
```java
// Main 클래스 생성
public class Main {
  int x; // 클래스 속성 생성

  // Main 클래스를 위한 생성자 생성
  public Main() {
    x = 5; // Main 클래스 객체 생성시 자동으로 x에 5 대입
  }

  public static void main(String[] args) {
    Main obj = new Main(); // Main 클래스의 객체 생성 (생성자 호출)
    System.out.println(obj.x); // 출력: 5
  }
}
```
  - 생성자의 이름은 클래스명과 동일해야하며 메서드의 반환값이 없어야함.
  - 생성자는 객체 생성 시에만 호출
  - 만약 생성자를 만들지 않았다면 기본 생성자가 컴파일할 때에 자동으로 부여됨.

## 기본 생성자
- 기본 생성자는 매개변수 또는 아무런 값이 안에 없으며 해당 클래스에 생성자가 없을 시 컴파일할 때 자동으로 생성됨.
```java
public class Main {

  public Main() {
    super(); // super에 대해서는 상속에 대해 배울때 보겠습니다.
  }
}
```

## 생성자 매개변수(Constructor Parameter)
- 생성자 또한 매개변수를 받을 수 있습니다.
```java
public class Main {
  int x;

  public Main(int y) {
    x = y;
  }

  public static void main(String[] args) {
    Main obj = new Main(5);
    System.out.println(obj.x); // 출력: 5
  }
}
```
- 매개변수의 숫자 또한 원하는 만큼 추가할 수 있습니다.
```java
public class Main {
  int modelYear;
  String modelName;

  public Main(int year, String name) {
    modelYear = year;
    modelName = name;
  }

  public static void main(String[] args) {
    Main myCar = new Main(1969, "Mustang");
    System.out.println(myCar.modelYear + ", " + myCar.modelName);
  }
}
// 출력: 1969, Mustang
```

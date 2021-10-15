---
title: "22&#46; Inheritance"
excerpt: "기본 자바"

categories:
  - 자바(기본)
tags:
  - 자바
  - java
  - basic
  - Inheritance
  - 상속
---

## 상속(Inheritance)
- 자바에서는 클래스의 메서드와 속성을 다른 클래스로 상속할 수 있습니다.
- 상속 관계는 2가지로 나눌 수 있습니다.
  - 자식클래스(subclass) - 다른 클래스로부터 상속 받음
  - 부모클래스(superclass) - 다른 클래스에 상속함
- `extends`라는 단어를 사용하여 상속을 받을 수 있습니다.
- Car 클래스는 자식클래스로 Vehicle 클래스는 부모클래스로 예를 들어보겠습니다.
```java
class Vehicle {
  protected String brand = "Ford"; // Vehicle 속성
  public void honk() { // Vehicle 메서드
    System.out.println("부릉부릉!");
  }
}
```
```java
class Car extends Vehicle {
  private String modelName = "Mustang"; // Car 속성

  public static void main(String[] args) {

    // MyCar 객체 생성
    Car myCar = new Car();

    // myCar 객체를 통해 Vehicle 클래스에 있는 honk() 메서드 호출
    myCar.honk();

    // Vehicle 클래스의 brand 속성과 Car 클래스의 modelName 속성 출력
    System.out.println(myCar.brand + " " + myCar.modelName);
  }
}
```
- 상속을 사용하는 이유
  - 코드 재사용이 용이함.
  - 다음에 배울 다형성에 필요함.

## 상수(final)
- 클래스가 상속하기를 원치 않는다면 class 앞에 `final`을 적으시면 됩니다.
```java
final class Vehicle {
  ...
}
class Car extends Vehicle {
  ...
}
// 상수는 상속 받지 못함으로 에러 발생
```

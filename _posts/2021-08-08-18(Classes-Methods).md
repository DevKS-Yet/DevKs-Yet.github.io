---
title: "18&#46; Classes Methods"
excerpt: "기본 자바"

categories:
  - 자바(기본)
tags:
  - 자바
  - java
  - basic
  - classes
  - methods
  - 클래스
  - 메서드
---

## 클래스 메서드(Class Methods)
- 클래스 메서드란 객체지향 프로그래밍에 대한 글을 올렸을 때 간략하게 브레이크, 전진, 후진으로 설명을 드렸었습니다. 이번에는 좀 더 자세히 알아보도록 하겠습니다.
- 클래스 메서드란 어떤 특정한 것을 실행하기 위해 사용됩니다.
```java
public class Main {
  static void myMethod() {
    System.out.println("Hello World!");
  }
}
```
- 메서드를 호출하기 위해서는 매서드명과 소괄호(`()`)와 세미콜론(`;`)을 적으면 됩니다.
```java
public class Main {
  static void myMethod() {
    System.out.println("Hello World!");
  }

  public static void main(String[] args) {
    myMethod(); // 출력: "Hello World!"
  }
}
```

## 정적과 비정(Static vs Non-Static)
- 자바 코드를 보다보면 메서드나 속성 앞에 `static` 또는 `public`이라는 단어가 있습니다.
- 위 예제에서는 `static` 메서드로 만들었습니다. 이 뜻은 클래스의 객체 생성 없이 바로 메서드를 실행 할 수 있습니다. 하지만 `public` 메서드로 생성 시에는 객체를 생성해야지만 메서드를 호출 할 수 있습니다.
```java
public class Main {
  // Static method
  static void myStaticMethod() {
    System.out.println("Static 메서드는 객체 생성 없이 호출 할 수 있습니다.");
  }

  // Public method
  public void myPublicMethod() {
    System.out.println("Public 메서드를 호출 하기 위해서는 객체를 생성해야합니다.");
  }

  // Main method
  public static void main(String[] args) {
    myStaticMethod(); // 정상적으로 메서드 호출 가능
    // myPublicMethod(); // 컴파일 에러

    Main obj = new Main(); // Main클래스의 객체 생성
    obj.myPublicMethod(); // 객체의 메서드 호출
  }
}
```
  - `public`과 `static`에 대해서는 후에 제어자에서 추가 설명하겠습니다.

## 매개변수(Parameter)
- 매개변수란 메서드 호출 시 넘겨주는 변수를 뜻합니다.
```java
public class Car {

  public void color(String carColor) {
    System.out.println("Car's color is " + carColor);
  }

  public static void main(String[] args) {
    Car myCar = new Car();
    myCar.color("black"); // call the color() method
  }
}
// 출력: Car's color is black
```

## 종합 예시
- 객체를 통한 메서드 호출 및 매개변수를 활용한 예시
```java
// Create Main class
public class Main {

  // Create a fullThrottle() method
  public void fullThrottle() {
    System.out.println("최대 속도로 달리고 있습니다.");
  }

  // Create a speed() method and add a parameter
  public void speed(int maxSpeed) {
    System.out.println("최대 속도는 " + maxSpeed + "입니다.");
  }

  // Inside main, call the methods on the myCar object
  public static void main(String[] args) {
    Main myCar = new Main(); // Create a myCar object
    myCar.fullThrottle(); // Call the fullThrottle() method
    myCar.speed(200); // Call the speed() method
  }
  // 출력: "최대 속도로 달리고 있습니다."
  // 출력: "최대 속도는 200입니다."
}
```
- 예시 실행 절차
  1. `Main`이라는 이름을 가진 클래스를 생성
  2. `Main` 클래스에 `fullThrottle()`과 `speed()` 메서드 생성
  3. 생성한 `fullThrottle()`과 `speed()`를 호출 시 글자가 출력되도록 정의
  4. `speed()` 메서드는 `maxSpeed`라는 `int`형 매개변수를 받게함
  5. `Main` 클래스의 메서드를 호출하기 위해서는 `Main` 클래스의 객체를 생성해야함
  6. `main()` 메서드 안에 `Main` 클래스의 객체 생성 (`main()` 메서드 안에 있는 코드만 실행 됨)
  7. `new`라는 단어를 통해 `myCar`이라는 이름을 가진 새로운 객체 생성
  8. `myCar`이라는 객체를 통해 `fullThrottle()`과 `speed()` 메서드를 호출 (호출 시에는 `.`을 통해 호출하며 또한 `speed()` 메서드는 `int`형의 매개변수를 주어야지 호출 가능)

## 다른 클래스에서 호출
- Main과 Second라는 클래스를 생성하여 Second에서 Main의 메서드를 호출해보겠습니다.
```java
public class Main {
  public void fullThrottle() {
    System.out.println("최대 속도로 달리고 있습니다.");
  }

  public void speed(int maxSpeed) {
    System.out.println("최대 속도는 " + maxSpeed + "입니다.");
  }
}
```
```java
class Second {
  public static void main(String[] args) {
    Main myCar = new Main(); // Create a myCar object
    myCar.fullThrottle(); // Call the fullThrottle() method
    myCar.speed(200); // Call the speed() method
  }
}
```

---
title: "23&#46; Abstraction"
excerpt: "기본 자바"

categories:
  - 자바(기본)
tags:
  - 자바
  - java
  - basic
  - abstraction
  - 추상
---

## 추상 클래스와 메서드(Abstract Classes and Methods)
- 추상 체이터란 구체적인 것들은 숨기고 필수적인 정보만 보여주는 것입니다.
- 추상은 추상 클래스 또는 인터페이스(interfaces)를 통해 구현할 수 있습니다.
- `abstract`은 비접근 제어자이며 클래스와 메서드에 사용할 수 있습니다.
  - 추상 클래스: 객체 생성이 제한되는 클래스 (객체를 생성하고자 한다면 반드시 상속받은 다른 클래스에서 생성 가능합니다.
  - 추상 메서드: 추상 클래스 안에서만 사용할 수 있으며 메서드가 정의되어 있지않아야함. 메서드의 정의는 자식클래스에서 할 수 있습니다.


- 예시
```java
// 추상 클래스
abstract class Animal {
  // 추상 메서드 (정의가 안되어있음)
  public abstract void animalSound();
  // 일반 메서드
  public void sleep() {
    System.out.println("Zzz");
  }
}
```
```java
// 자식 클래스
class Ping extends Animal {
  public void animalSound() {
    // animalSound는 여기서 정의함
    System.out.println("꾸익꾸익~");
  }
}
```
```java
// 메인 클래스
class Main {
  public static void main(String[] args) {
    Pig myPig = new Pig();
    myPig.animalSound();
    myPing.sleep();
  }
}
```

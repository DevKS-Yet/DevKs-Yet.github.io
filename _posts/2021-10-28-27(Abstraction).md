---
title: "27&#46; Abstraction"
excerpt: "기본 자바"

categories:
  - 자바(기본)
tags:
  - 자바
  - java
  - basic
  - abstraction
  - 추상 클래스
---

## 추상 클래스와 메소드(Abstract Classes and Methods)
- 데이터 추상화는 유저에게 필수 정보 외에는 숨기기 위한 방법입니다.
- 추상 클래스 또는 인터페이스를 통해 추상화를 할 수 있습니다.
- `abstract`는 접근제어자가 아니며 클래스와 메소드에 적용할 수 있습니다.
  - 추상 클래스 : 객체를 생성이 제한된 클래스 (사용하기 위해서는 다른 클래스에 상속을 해야함)
  - 추상 메소드 : 추상 클래스에서만 사용이 가능하며 메소드 내부가 정의되어 있지 않다. 함수 정의는 상속 받은 클래스에서 합니다.
- 추상 클래스는 추상 메소드와 일반 메소드를 갖을 수 있습니다.

```java
abstract class Animal {
  // 추상 메소드
  public abstract void animalSound();

  // 일반 메소드
  public void sleep() {
    System.out.println("Zzz");
  }
}
```
```java
Animal myObj = new Animal(); // 에러 발생
```
```java
// 자손 클래스
class Pig extends Animal {
  public void animalSound() {
    // 여기서 animalSound()를 정의함
    System.out.println("The pig says: wee wee");
  }
}
```
```java
class Main {
  public static void main(String[] args) {
    Pig myPig = new Pig(); // Create a Pig object
    myPig.animalSound();
    myPig.sleep();
  }
}
```

## 언제 왜 추상 클래스와 메소드를 사용하나요?
- 보안성 - 상세 내용은 숨기고 객체의 필수적인 정보만 보여주기 위해

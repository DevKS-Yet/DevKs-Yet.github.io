---
title: "25&#46; polymorphism"
excerpt: "기본 자바"

categories:
  - 자바(기본)
tags:
  - 자바
  - java
  - basic
  - polymorphism
  - 다형성
---

## 다형성(polymorphism)
- 다형성은 다양한 형태를 뜻하며 상속을 통해 많은 클래스가 연결되어있는 경우에 발생합니다.
- 이전 포스트에서 상속을 통해 다른 클래스로 변수와 메소드를 상속시킬 수 있었습니다. 다형성은 상속시킨 메소드들을 다른 곳에서도 사용을 하게끔하는 것입니다. 이것을 통해 하나로 다양한 방향으로 동작할 수 있게합니다.
```java
class Animal {
  public void animalSound() {
    System.out.println("The animal makes a sound");
  }
}
```
```java
class Pig extends Animal {
  public void animalSound() {
    System.out.println("The pig says: wee wee");
  }
}
```
```java
class Dog extends Animal {
  public void animalSound() {
    System.out.println("The dog says: bow wow");
  }
}
```
```java
class Main {
  public static void main(String[] args) {
    Animal myAnimal = new Animal(); // Animal 객체 생성
    Animal myPig = new Pig(); // Pig 객체 생성
    Animal MyDog = new Dog(); // Dog 객체 생성
    myAnimal.animalSound();
    myPig.animalSound();
    MyDog.animalSound();
  }
}
```

## 왜, 언제 상속과 다형성을 사용하면 될까요?
- 코드 재사용에 용이합니다.

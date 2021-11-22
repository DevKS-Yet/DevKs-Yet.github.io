---
title: "26&#46; Inner Classes"
excerpt: "기본 자바"

categories:
  - 자바(기본)
tags:
  - 자바
  - java
  - basic
  - Inner Classes
  - 내부 클래스
---

## 내부 클래스(Inner Classes)
- 자바에서는 클래스 중첩이 가능합니다. 중첩 클래스의 목적은 클래스들을 하나로 묶어 코드의 가독성과 유지를 높이기 위함입니다.
- 내부 클래스를 실행하고자 한다면 외부 클래스에 객체를 만든 후 내부 클래스의 객체를 만들면 됩니다.

```java
class OuterClass {
  int x = 10;

  class InnerClass {
    int y = 5;
  }
}
```
```java
public class Main {
  public static void main(String[] args) {
    OuterClass myOuter = new OuterClass();
    OuterClass.InnerClass myInner = myOuter.new InnerClass();
    System.out.println(myInner.y + myOuter.x);
  }
}

// 결과: 15
```

## 프라이빗 내부 클래스(Private Inner Class)
- 일반적인 클래스와는 달리 내부 클래스는 `private` 또는 `proected` 으로 설정이 가능합니다. 만약 외부 객체를 통해 내부 클래스를 접근을 제한하고자 한다면 `private`으로 내부 클래스를 선언하면 됩니다.

```java
class OuterClass {
  int x = 10;

  private class InnerClass {
    int y = 5;
  }
}
```
```java
public class Main {
  public static void main(String[] args) {
    OuterClass myOuter = new OuterClass();
    OuterClass.InnerClass myInner = myOuter.new InnerClass();
    System.out.println(myInner.y + myOuter.x);
  }
}

// 결과: 에러
```

## 스태틱 내부 클래스(Static Inner Class)
- 내부 클래스는 스태틱일 수도 있습니다. 외부 클래스 객체 생성 없이 바로 접근을 할 수 있습니다.

```java
class OuterClass{
  int x = 10;

  static class InnerClass {
    int y = 5;
  }
}
```
```java
public class Main {
  public static void main(String[] args) {
    OuterClass.InnerClass myInner = new OuterClass.InnerClass();
    System.out.println(myInner.y);
  }
}

// 결과: 5
```

## 내부 클래스에서 외부 클래스에 접근하기
- 내부 클래스의 장점 중 하나는 외부 클래스에 접근이 가능하다는 것입니다.

```java
class OuterClass {
  int x = 10;

  class InnerClass {
    public int myInnerMethod() {
      return x;
    }
  }
}
```
```java
public class Main {
  public static void main(String[] args) {
    OuterClass myOuter = new OuterClass();
    OuterClass.InnerClass myInner = myOuter.new InnerClass();
    System.out.println(myInner.myInnerMethod());
  }
}

// 결과: 10
```

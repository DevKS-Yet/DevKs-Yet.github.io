---
title: "21&#46; Encapsulation"
excerpt: "기본 자바"

categories:
  - 자바(기본)
tags:
  - 자바
  - java
  - basic
  - encapsulation
  - 캡슐화
---

## 캡슐화(Encapsulation)
- 캡슐화란 중요한 정보를 유저로부터 숨기는 것을 뜻합니다.
- 캡슐화를 하기 위해서는
  - 클래스 변수/속성을 `private`으로 선언
  - get과 set 메서드를 생성하여 메서드를 통해 `private` 변수에 접근할 수 있도록 제공

## Get과 Set
- 접근제어자에서 `private` 변수는 오직 같은 클래스에서만 접근이 허용된다고 했습니다. 하지만 get과 set 메서드를 제공함으로 다른 클래스에서도 접근할 수 있습니다.
- get 메서드는 변수값을 반환하고 set 메서드는 변수값을 설정해줍니다.
- 이름은 두 메서드 다 get 또는 set으로 시작합니다. 그리고 뒤에 첫 글자는 대문자인 변수명이 붙습니다.
```java
public class Car {
  private String carModel;

  // Getter
  public String getCarModel() {
    return carModel;
  }

  // Setter
  public void setCarModel(String newCarModel) {
    this.carModel = newCarModel;
  }
}
```
  - `this.carModel`에서 `this`를 사용함으로 Car 객체의 carModel 속성을 가리키고 있다는 것을 인지시켜줍니다.
  - `this`를 사용함으로 매개변수와 객체의 속성명이 같아도 구분하여 프로그래밍을 할 수 있습니다.
  ```java
  public class Car {
    private String name;

    // Setter
    public void setName(String name) {
      this.name = name; // 매개변수 name과 클래스 변수 name이 구분됨
    }
  }
  ```
- 위와 같이 Car이 설정되었다면 다른 클래스에서도 Getter와 Setter를 통해 불러올 수 있습니다.
```java
public class Main {
  public static void main(String[] args) {
    Car obj = new Car();
    // obj.carModel = "Volvo"; // error
    // System.out.println(obj.carModel); // error

    obj.setCarModel("Volvo");
    System.out.println(obj.getCarModel());
  }
}
```

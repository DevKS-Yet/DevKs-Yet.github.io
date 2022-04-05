---
title: "자바의 정석 4일차"
excerpt: "post"

categories:
- standard-of-java
tags:
- java
- book
---

# Chapter 02 변수(Variable)

## 3. 기본형(primitive type)
드디어 모두가 꿈꾸는 컴퓨터 = 데이터 통신에서 가장 중요한 기본 데이터 타입에 대해서 작성하였다.  
지금 당장 달달 외우라는 소리는 절대로 하지 않는다. 어차피 자주 사용하기 때문에 코드를 치면서 외워질 것이다.

### 4.1 논리형 - boolean
`boolean`은 `true`와 `false`만 있는 데이터 타입이며 아무런 값을 주지 않았을 경우 기본값은 `false`이다.  
앞서 언급한 것처럼 `boolean`은 논리구현에 자주 사용이 된다. 예를 들어 TV 전원버튼 온오프 기능을 생각하면 좋겠다.

`boolean`의 선언 방법과 사용 용도는 아래와 같다.
```java
boolean power = true;

void power() {
    power = !power;  // 이러면 매우 간단하게 사용이 가능한데 굳이 지금 알 필요 없다. 추후 다시 나온다.
  }
```

다만 주의할 점은 자바에서는 대소문자가 구별되기 때문에 TRUE와 true는 다르다! 그래도 예약어는 혼동될 수 있으니 변수로서 사용은 자제하자.

### 4.2 문자형 - char
문자형으로는 `char`만 있다. `String`이 기본형 문자형이라고 하시는 분들은 2일차에 한 부분을 보고오라고 하고 싶지만 간략하게 언급을 했기에 다시 설명하겠다. `String`은 참조형 변수이며 `String sentence = "This is sentence"`와 같이 선언이 가능한 이유는 자바가 일일이 객체 만드는 것이 안쓰러워서 특별히 추가해준 것이다.

이야기가 조금 엇나갔는데 다시 `char`의 설명으로 가자면 char타입의 변수는 단 하나의 문자만을 저장할 수 있다. 방법은 아래와 같다.  
```java
char ch = 'A';  // 문자 'A'를 char타입의 변수 ch에 저장. 'A'는 아스키코드로 65다. 그러므로 저장도 65로 되고 정수 또는 실수와 더한다면 65로 대입이 된다.
char ch1 = 65;  // 위와 아래와 동일
```

###### 특수 문자 다루기

`char`형에는 영문자 외에 스페이스나 줄바꿈 등과 같은 특수문자도 저장할 수 있다.  
해당 문자들은 아래와 같다

| 특수문자 | 문자 리터럴 |
|:---|:---|
| tab | \t |
| backspace | \b | 
| form feed | \f |
| new line | \n |
| carriage return | \r |
| single quotation mark | \' |
| double quotation mark | \" |
| backslash | \\ |
묘한 것이 있다. 분명 `char`형은 문자 하나만 저장할 수 있다고 했지만 보면 특수문자는 2개로 이루어져있다. 하지만 컴퓨터는 해당 특수문자를 한 문자로 이해한다.

##### 예제 2-8/ch2/SpecialCharEx.java
해당 예제는 책에 있는 것과 다르게 새로 만들었다.
```java
class SpecialCharEx {
    public static void main(String[] args) {
        System.out.println("\\t - this is just a \t example");
        System.out.println("\\b - this is just a \b example");
        System.out.println("\\f - this is just a \f example");
        System.out.println("\\n - this is just a \n example");
        System.out.println("\\r - this is just a \r example");
        System.out.println("\\\' - this is just a \' example");
        System.out.println("\\\" - this is just a \" example");
        System.out.println("\\\\ - this is just a \\ example");
    }
}
```
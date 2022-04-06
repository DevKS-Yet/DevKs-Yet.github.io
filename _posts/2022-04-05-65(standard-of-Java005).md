---
title: "자바의 정석 5일차"
excerpt: "post"

categories:
- standard-of-java
tags:
- java
- book
---

# Chapter 02 변수(Variable)

## 4. 기본형(primitive type)
어제에 이어서 오늘은 Chapter 02를 끝내보자


### 4.4 실수형

###### 실수형의 범위와 정밀도
실수형은 실수를 저장하기 위한 타입으로 float와 double이 있으며 상세 스펙은 아래를 참고하길 바란다.

| 타입 | 저장 가능한 값의 범위(양수) | 정밀도 | 크기(byte) |
|:---:|:---:|:---:|:---:|
| float | ±(1.4E-45 ~ 3.4E38) | 7자리 | 4 |
| double | ±(4.9E-324 ~ 1.8E308) | 15자리 | 8 |

float는 -1.3E-45 ~ 1.3E45의 범위를 표현할 수 없다(0은 제외). 그 이유로는 저장하는 형식이 다르기 때문이다.

정수형은 부호용으로 1bit를 사용하고 나머지 bit로 숫자를 표현하였다. 하지만 실수형은 부호용 1bit를 제외한 나머지 bit를 지수, 가수 부분으로 나누어서 저장한다.  
그렇기 떄문에 오버플로우와 정수형에는 없는 언더플로우가 있는데 한번 찾아보고 넘어가자.

실수형 값을 저장할 때, float타입이 아닌 double타입의 변수를 사용하는 경우는 대부분 저장하려는 값의 범위 떄문이 아니라 높은 정밀도가 필요해서이다.  
연산속도의 향상이나 메모리를 절약하려면 float를 선택하고, 더 큰 값의 범위라던가 더 높은 정밀도를 필요로 한다면 double을 선택하자.

##### 예제 2-10/ch2/FloatEx1.java
```java
class FloatEx1 {
    public static void main(String[] args) {
        float f1 = 9.12345678901234567890f;
        float f2 = 1.2345678901234567890f;
        double d1 = 9.12345678901234567890d;

        System.out.println("\t   12345678901234");
        System.out.printf("f1 : %f%n", f1);
        System.out.printf("f1 : %24.20f%n", f1);
        System.out.printf("f2 : %24.20f%n", f2);
        System.out.printf("d1 : %24.20f%n", d1);
    }
}
```
위 예제를 실행해보면 float타입 경우 들어간 값과 출력된 값이 다르다는걸 알 수 있다. float타입의 정밀도는 7임으로 7자리까지만 맞고 나머지는 오차가 생긴다.

###### 실수형의 저장형식
앞서 언급한 것과 같이 실수형의 저장형식은 정수형과 다르다. 부호(Sign), 지수(Exponent), 가수(Mantissa)로 나뉘어져있는데 이 부분도 따로 찾아보길 권한다.



## 5. 형변환


### 5.1 형변환이란?
형변환이란, 변수 또는 상수의 타입을 다른 타입으로 변환하는 것을 뜻한다. 예를 들어서 int형으로 5를 저장했는데 2로 나누며 실수가 된다. int는 정수만 받음으로 0.5가 사라진다. 그렇다면 float 또는 double로 바꿔서 저장을 하면 된다.


### 5.2 형변환 방법
형변환 방법은 아래와 같다.
```java
//(타입)피연산자
double d = 85.4;
int score = (int)d;  // 실수형을 정수형으로 변환. 당연히 소수점 부분은 사라진다.
```

##### 예제 2-12/ch2/CastingEx1.java
```java
class CastingEx1 {
    public static void main(String[] args) {
        double d = 85.4;
        int score = (int) d;

        System.out.println("score = " + score);
        System.out.println("d = " + d);
    }
}
```

기본형에서는 boolean을 제외한 나머지 타입들은 서로 형변환이 가능하다. 참조형과 기본형간의 형변환은 불가능이다.


### 5.3 정수형간의 형변환
큰 타입에서 작은 타입으로 변환하면 값손실이 있다. 하지만 신기하게도 작은 타입에서 큰 타입으로 변경 시 값손실이 없다. 양수일 경우에는 값손실이 없을 수 있는데 음수일 경우는 왜 값손실이 없는 것일까? 하는 분들이라면 2의 보수법을 한번 보는 걸 추천한다. ~~사실 몰라도 괜찮을거같다.~~

##### 예제 2-13/ch2/CastingEx2.java
```java
class CastingEx2 {
    public static void main(String[] args) {
        int i = 10;
        byte b = (byte) i;  // (Narrowing Casting)
        System.out.printf("[int -> byte] i=%d -> b=%d%n", i, b);
        
        i = 300;
        b = (byte) i;
        System.out.printf("[int -> byte] i=%d -> b=%d%n", i, b);
        
        b = 10;
        i = (int) b;  // 사실 작은 타입에서 큰 타입으로 갈때는 자동적으로 형변환을 해준다(Widening Casting).
        System.out.printf("[int -> byte] i=%d -> b=%d%n", i, b);
        
        b = -2;
        i = (int) b;
        System.out.printf("[int -> byte] i=%d -> b=%d%n", i, b);

        System.out.println("i = " + Integer.toBinaryString(i));  // 2진 정수를 볼 수 있다. 추천 안함
    }
}
```


### 5.4 실수형 간의 형변환
실수형도 정수형처럼 형변환이 가능하다. 다만 실수형에서는 float타입의 범위를 넘는 값을 float로 형변환하는 경우에 ±무한대 또는 0을 얻을 수 있다.

##### 예제 2-14/ch2/CastingEx3.java
```java
class CastingEx3 {
    public static void main(String[] args) {
        float f1 = 9.1234567f;
        double d1 = 9.1234567;  // double형은 리터럴 뒤에 d를 안적어도 된다. 문의는 자바에 하자
        double d2 = (double) f;

        System.out.printf("f1 = %20.18f%n", f1);
        System.out.printf("d1 = %20.18f%n", d1);
        System.out.printf("d2 = %20.18f%n", d2);
    }
}
```


### 5.5 정수형과 실수형 간의 형변환
정수형과 실수형은 저장형식이 완전히 다르다. 그렇기 때문에 정수형에서 정수형 또는 실수형에서 실수형의 형변환 과정보다 복잡한 과정을 거친다.  
이 부분은 따로 공부하자. ~~사실 나도 모르고 개발했었다... 부끄럽네...... 그래서 다시 공부하는 중이다.~~

##### 예제 2-15/ch2/CastingEx4.java
```java
class CastingEx4 {
    public static void main(String[] args) {
      int i1 = 91234567;
      float f1 = (float) i1;
      int i2 = (int) f1;

      double d1 = (double) i1;
      int i3 = (int) d1;

      float f2 = 1.666f;
      int i4 = (int) f2;

      System.out.printf("i1 = %d\n", i1);
      System.out.printf("f1 = %f\ti2 = %d\n", f1, i2);
      System.out.printf("d1 = %f\ti3 = %d\n", d1, i3);
      System.out.printf("(int) %f = %d%n", f2, i4);
    }
}
```


### 5.6 자동 형변환
위에서 살짝 언급했지만 자동적으로 형변환이 되는 규칙이 있다.

###### 자동 형변환의 규칙
컴파일러는 기존의 값을 최대한 보존할 수 있는 타입으로 자동 형변환을 한다.
크게는 정수형에서 실수형으로 자동 형변환을 해주며 정수형 안에서는 `byte -> short || char -> int -> long`순으로 자동 변환이 가능하고 실수형에서는 `float -> double`로 자동 형변환이 된다.

다만 정수형을 실수형으로 형변환하는 경우, 정밀도의 한계로 인한 오차가 발생할 수 있다.


### 정리
- boolean을 제외한 나머지 7개의 기본형은 서로 형변환이 가능하다.
- 기본형과 참조형은 서로 형변환할 수 없다.
- 서로 다른 타입의 변수간의 연산은 형변환을 하는 것이 원칙이지만, 값의 범위가 작은 타입에서 큰 타입으로의 형변환은 생략할 수 있다.

> 드디어 chapter 02가 끝났다. 그 다음장은 연산자에 대해서 다루며 개인적으로 변수가 이해하기 더 어려웠다.  
> 앞으로도 힘내서 나도 개발로 내 집을 꾸며보자... 젭알 자동화 집 만들고싶다
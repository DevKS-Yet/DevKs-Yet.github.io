---
title: "자바의 정석 6일차"
excerpt: "post"

categories:
- standard-of-java
tags:
- java
- book
---

# Chapter 03 연산자(Operator)

## 1. 연산자(operator)
연산자라는 것은 간단하게 사칙연산 등을 뜻한다.


### 1.1 연산자와 피연산자
- 연산자(operator) : 연산을 수행하는 기호 (`+, -, *, / 등`)
- 피연산자(operand) : 연산 당하는 애들(변수, 상수, 리터럴, 수식)


### 1.2 식(expression)과 대입연산자
식은 수학 시간에도 많이 보았을 것이다(예: `4 * x + 3`).  
그리고 식 마지막에는 `;`를 붙여서 문장으로 만들어야지 프로그램이 하나의 식으로 이해한다.

대입연산자라는 것은 위의 식에서 특정 값을 얻었다고 하자. 하지만 아무데도 저장되지 않았기에 쓸모없다.  
저장하기 위해서 대입연산자를 사용한다(예: `y = 4 * x + 3`).  
위와 같이 함으로써 `4 * x + 3`의 값이 `y`에 저장된다.


### 1.3 연산자의 종류
연산자의 종류는 조금 많다. ~~귀찮으니 타블로그 ㄱㄱ~~ 아래 테이블을 참고하길 바란다.

| 우선순위 | 종류 | 연산자 | 설명 |
|:---:|:---:|:---:|:---:|
| 1 | 증감 연산자 | ++, -- | 1씩 증가 또는 감소 |
| 2 | 산술 연산자 | +, -, *, /, % | 사칙연산과 나머지 연산(%;mod) |
| 3 | 쉬프트 연산자 | <<, >>, <<<, >>> | bit값을 이동 |
| 4 | 비교 연산자 | <, >, <=, >=, ==, != | 크고 작음과 같고 다름을 비교 |
| 5 | 비트 연산자 | &amp;, &#124;, ^, ~ | bit and/or/xor/not 연산을 한다(~는 1순위) |
| 6 | 논리 연산자 | &&, &#124;&#124;, ! | and/or/not으로 조건을 연결(!는 1순위) |
| 7 | 조건(삼항) 연산자 | ?, : | 짧게 쓴 1차적 이프문 |
| 8 | 대입 연산자 | =, +=, -=, *=, /=, %= | 우변의 값을 좌변에 저장 |

보면 대입 연산자가 가장 마지막 순위이기 때문에 모든 좌변의 식이 끝난 후에 실행 된다. 한국인은 책을 왼쪽에서 오른쪽으로 읽지만 컴퓨터는 식(거시적으로)을 오른쪽에서 왼쪽으로 읽는다고 생각하고 넘어가자.  
기왕 적는거 순위와 쉬프트/비트 연산자 까지 적었는데 일반적으로 쓸 일 없었다. 게임이나 알고리즘쪽으로 간다고 하면 필요할지도 모른다.


### 1.4 연산자의 우선순위와 결합규칙
위에 적은 우선순위 중에서도 동일한 우선순위를 가진 연산자 안에서도 순위가 나뉜다. 이건 궁금하면 직접 찾아보자. ~~절대로 귀찮아서 그런거 아니다. 필요가 없기 때문이다.~~


### 1.5 산술 변환(usual arithmetic conversion)
아까 말한 정수형끼리 또는 실수형끼리 또는 정수형과 실수형 간의 형변환을 말하는 것이다. 다 필요없고 자동 형변환 하는 두가지 규칙만 읽고 넘어가자
1. 두 피연산자의 타입을 같게 일치시킨다(보다 큰 타입으로 일치).
2. 피연산자의 타입이 int보다 작은 타입이면 int로 변환된다.


## 2. 단항 연산자
이 부분은 예제만 적고 넘어가겠다. 궁금한 것이 있다면 댓글~~지금은막혀있지만데헷~~ 또는 구글만이 답이다.

### 2.1 증감 연산자 ++ --

##### 예제 3-1/ch3/OperatorEx1.java
```java
class OperatorEx1 {
    public static void main(String[] args) {
        int i = 5;
        i++;
        System.out.println(i);
        
        i = 5;
        ++i;
        System.out.println(i);
    }
}
```

##### 예제 3-2/ch3/OperatorEx2.java
```java
class OperatorEx2 {
    public static void main(String[] args) {
        int i=5, j=0;
        
        j = i++;
        System.out.println("j = i++; 실행 후, i = " + i + ", j = " + j);
        
        i = 5;
        j = 0;
        
        j = ++i;
        System.out.println("j = ++i; 실행 후, i = " + i + ", j = " + j);
    }
}
```
이 예제는 이해가 잘 안갈 수 있다. 꼭 구글에서 찾아보자

##### 예제 3-3/ch3/OperatorEx3.java
```java
class OperatorEx3 {
    public static void main(String[] args) {
        int i=5, j=5;
        System.out.println(i++);
        System.out.println(++j);
        System.out.println("i = " + i + ", j = " + j);
    }
}
```


### 2.2 부호 연산자 + -

##### 예제 3-4/ch3/OperatorEx4.java
```java
class OperatorEx4 {
    public static void main(String[] args) {
        int i = -10;
        i = +i;
        System.out.println(i);
        
        i = -10;
        i = -i;
        System.out.println(i);
    }
}
```


## 3. 산술 연산자

### 3.1 사칙 연산자 + - * /

##### 예제 3-5/ch3/OperatorEx5.java
```java
class OperatorEx5 {
    public static void main(String[] args) {
        int a=10, b=4;

        System.out.printf("%d + %d = %d%n", a, b, a + b);
        System.out.printf("%d - %d = %d%n", a, b, a - b);
        System.out.printf("%d * %d = %d%n", a, b, a * b);
        System.out.printf("%d / %d = %d%n", a, b, a / b);
        System.out.printf("%d / %f = %f%n", a, (float) b, a / (float) b);
    }
}
```

##### 예제 3-6/ch3/OperatorEx6.java
```java
class OperatorEx6 {
    public static void main(String[] args) {
        byte a=10, b=20;
        byte c = a + b;  // 여긴 에러가 뜰텐데 한번 고쳐보자
        System.out.println(c);
    }
}
```

##### 예제 3-7/ch3/OperatorEx7.java
```java
class OperatorEx7 {
    public static void main(String[] args) {
        byte a=10, b=30;
        byte c = (byte) (a * b);
        System.out.println(c);  // 정답이 이상할텐데 당연한 것이다.
    }
}
```


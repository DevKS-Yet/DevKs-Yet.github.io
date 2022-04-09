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

##### 예제 3-8 / ch3/OperatorEx8.java
```java
class OperatorEx8 {
    public static void main(String[] args) {
        int a = 1_000_000;
        int b = 2_000_000;
        
        long c = a * b;

        System.out.println(c);
    }
}
```
위의 예제의 결과는 2_000_000_000_000이 아닌 -1454759936이다. 이유는 연산 결과가 int형으로 되었기 때문이다.  
올바른 결과를 얻으려면 우변에 long형으로 형변환을 해주어야한다(`ling c = (long) a * b`).

##### 예제 3-9/ch3/OperatorEx9.java
```java
class OperatorEx9 {
    public static void main(String[] args) {
        long a = 1_000_000 * 1_000_000;
        long b = 1_000_000 * 1_000_000L;

        System.out.println("a = " + a);
        System.out.println("b = " + b);
    }
}
```
예제 3-8과 동일한 이유로 출력 값이 다르다.

##### 예제 3-10/ch3/OperatorEx10.java
```java
class OperatorEx10 {
    public static void main(String[] args) {
        int a = 1_000_000;
        
        int result1 = a * a / a;
        int result2 = a / a * a;

        System.out.printf("%d * %d / %d = %d%n", a, a, a, result1);
        System.out.printf("%d * %d / %d = %d%n", a, a, a, result2);
    }
}
```

##### 예제 3-11/ch3/OperatorEx11.java
```java
class OperatorEx11 {
    public static void main(String[] args) {
        char a = 'a';
        char d = 'd';
        char zero = '0';
        char two = '2';

        System.out.printf("'%c' - '%c' = %d%n", d, a, d - a);
        System.out.printf("'%c' - '%c' = %d%n", two, zero, two - zero);
        System.out.printf("'%c' = %d%n", a, (int)a);
        System.out.printf("'%c' = %d%n", d, (int)d);
        System.out.printf("'%c' = %d%n", zero, (int)zero);
        System.out.printf("'%c' = %d%n", two, (int)two);
    }
}
```
결과값은 숫자와 영문자의 유니코드를 보면 좀 더 쉽게 이해가 가능하다

##### 예제 3-12/ch3/OperatorEx12.java
```java
class OperatorEx12 {
    public static void main(String[] args) {
        char c1 = 'a';
        char c2 = c1;
        char c3 = ' ';
        
        int i = c1 + 1;
        c3 = (char) (c1 + 1);
        c2++;
        c2++;

        System.out.println("i = " + i);
        System.out.println("c2 = " + c2);
        System.out.println("c3 = " + c3);
    }
}
```

##### 예제 3-13/ch3/OperatorEx13.java
```java
class OperatorEx13 {
    public static void main(String[] args) {
        char c1 = 'a';
        
//        char c2 = c1+1;  // 컴파일 에러
        char c2 = 'a' + 1;

        System.out.println(c2);
    }
}
```
위 에제를 보면 살짝 이상하다. c1에서 1을 더한 값이 존재하는데 컴파일 에러라고 뜬다. 그 이유는 (c1+1)은 변수와 리터럴 간의 연산이고 ('a'+1)은 리터럴 간의 연산이기에 후자는 자동으로 형변환이 가능한 것이다.

##### 예제 3-14/ch3/OperatorEx14.java
```java
class OperatorEx14 {
    public static void main(String[] args) {
        char c = 'a';
        for (int i=0; i<26; i++) {
            System.out.print(c++);
        }
        System.out.println();
        
        c = 'A';
        for (int i=0; i<26; i++) {
            System.out.print(c++);
        }
        System.out.println();
        
        c = '0';
        for (int i=0; i<10; i++) {
            System.out.print(c++);
        }
        System.out.println();
    }
}
```

##### 예제 3-15/ch3/OperatorEx15.java
```java
class OperatorEx15 {
    public static void main(String[] args) {
        char lowerCase = 'a';
        char upperCase = (char)(lowerCase - 32);  // 변수와 리터럴 간의 계산이기에 형변환을 해야한다.
        System.out.println(upperCase);
    }
}
```

##### 예제 3-16/ch3/OperatorEx16.java
```java
class OperatorEx16 {
    public static void main(String[] args) {
        float pi = 3.141592f;
        float shortPi = (int) (pi * 1000) / 1000f;
        System.out.println(shortPi);
    }
}
```
위 예제를 통해서 소수점을 원하는 자리수에서 자를 수 있으니 알아두면... 쓸 일은 그닥 없지만 알아두자...

##### 예제 3-17/ch3/OperatorEx17.java
```java
class OperatorEx17 {
    public static void main(String[] args) {
        double pi = 3.141592;
        double shortPi = (int) (pi * 1000 + 0.5) / 1000.0;
        System.out.println(shortPi);
    }
}
```
0.5를 더해줌으로서 반올림을 할 수 있다. 내림은 예제 3-16에서 한것과 동일하고 올림은 어떻게하면 좋을지 생각해보자. 예제로는 안나오는거 같더라

##### 예제 3-18/ch3/OperatorEx18.java
```java
class OperatorEx18 {
    public static void main(String[] args) {
        double pi = 3.141592;
        double shortPi = Math.round(pi * 1000) / 1000.0;
        System.out.println(shortPi);
    }
}
```
Math 객체의 round 메서드는 소수 첫째 자리를 반올림 시켜준다. 예제 3-16과 17처럼 할 수도 있지만 Math 객체의 메서드를 사용하면 더 편하다.

### 3.2 나머지 연산자 %
나머지 연산자란 왼쪽의 피연산자를 오른쪽 피연산자로 나누고 난 나머지 값을 결과로 반환하는 연산자이다. 예는 아래와 같다

##### 예제 3-19/ch3/OperatorEx19.java
```java
class OperatorEx19 {
    public static void main(String[] args) {
        int x = 10;
        int y = 8;

        System.out.printf("%d을 %d로 나누면, %n", x, y);
        System.out.printf("몫은 %d이고, 나머지는 %d입니다.%n", x / y, x % y);
    }
}
```
위 예제의 x와 y의 값을 바꿔가면서 실행해보면 나머지 연산자에 대해 쉽게 알 수 있을 것이다.

##### 예제 3-20/ch3/OperatorEx20.java
```java
class OperatorEx20 {
    public static void main(String[] args) {
        System.out.println(-10%8);
        System.out.println(10%-8);
        System.out.println(-10%-8);
    }
}
```
나머지 연산자는 나누는 수로 음수도 허용한다.


## 4. 비교 연산자
비교 연산자는 두 피연산자를 비교하는데 사용되는 연산자다. 연산 결과는 오직 true와 false 둘 중의 하나이다.

### 4.1~2 대소/등가비교 연산자

| 비교연산자 | 연산결과 |
|:---:|:---|
| > | 좌변 값이 크면, true 아니면 false |
| < | 좌변 값이 작으면, true 아니면 false |
| >= | 좌변 값이 크거나 같으면, true 아니면 false |
| <= | 좌변 값이 작거나 같으면, true 아니면 false |
| == | 두 값이 같으면, true 아니면 false |
| != | 두 값이 다르면, true 아니면 false |

##### 예제 3-21ch3/OperatorEx21.java
```java
class OperatorEx21 {
    public static void main(String[] args) {
        System.out.printf("10 == 10.0f \t %b%n", 10==10.0f);
        System.out.printf("'0' == 0 \t %b%n", '0'==0);
        System.out.printf("'A' == 65 \t %b%n", 'A'==65);
        System.out.printf("'A' > 'B' \t %b%n", 'A' > 'B');
        System.out.printf("'A'+1 != 'B' \t %b%n", 'A'+1 != 'B');
    }
}
```

---
title: "자바의 정석 8일차"
excerpt: "post"

categories:
- standard-of-java
tags:
- java
- book
---

# Chapter 04 조건문과 반복문(if, switch, for, while statement)
조건문과 반복문은 처음 접하는 사람에게는 어렵다기보다는 익숙하지 않을 수 있다. 그렇기에 많이 보는 것도 중요하지만 직접 뭔가를 생각해서 만들어보는 것이 가장 좋은 방법이라고 생각한다.

아재 우리는 순차적으로만 실행했던 코드를 제어문(조건문과 반복문)을 통해 프로그램의 흐름을 바꿔보자

## 1. 조건문 - if, switch
조건문은 조건식과 문장을 포함하는 블럭{}으로 구성되어 있으며, 조건식의 연산결과에 따라 실행할 문장이 달라져서 프로그램의 실행흐름을 변경할 수 있다.


### 1.1 if문
if문은 가장 기본적인 조건문이며 만일이라는 뜻으로 조건식이 참이면 괄호{} 안의 문장들을 수행한다.

```java
if (조건식) {
    // 조건식이 참(true)일 때 수행될 문장들을 적는다.
}
```

이런 식이며 예를 들어서 만약 60점 이상인 사람이 합격이라고 출력 시키고 싶다면

```java
if (score >= 60 ) {
    System.out.println("합격입니다.");
}
```
라고 코드를 작성하면 score가 60점 이상만 합격이라고 출력한다.

###### 조건식
if문에 사용되는 조건식은 일반적으로 비교연산자와 논리연산자로 구성된다. 기억이 안난다면 6일차와 7일차를 빠르게 보고 오자.

##### 예제 4-1/ch4/FlowEx1.java
```java
class FlowEx1 {
    public static void main(String[] args) {
        int x = 0;
        System.out.printf("x=%d 일때, 참인 것은%n", x);
        
        if (x == 0) System.out.println("x == 0");  // if문 괄호 안에 수행될 것이 하나라면 괄호 없이 써도 된다.
        if (x != 0) System.out.println("x != 0");
        if (!(x == 0)) System.out.println("!(x == 0)");
        if (!(x != 0)) System.out.println("!(x != 0)");
        
        x = 1;
        System.out.printf("x = %d 일때, 참인 것은%n", x);
        
        if (x == 0) System.out.println("x == 0");
        if (x != 0) System.out.println("x != 0");
        if (!(x == 0)) System.out.println("!(x == 0)");
        if (!(x != 0)) System.out.println("!(x != 0)");
    }
}
```
위 예제에서는 괄호{}가 안보여서 뭐지라고 생각할 수 있지만 주석으로도 적었듯이 수행할 것이 하나(`;`로 구별)라면 괄호 없이 적어도 된다.

##### 예제 4-2/ch4/FlowEx2.java
```java
import java.util.*;  // Scanner 클래스를 사용하기 위함. 후에 자주 볼것임

class FlowEx2 {
    public static void main(String[] args) {
        int input;

        System.out.println("숫자를 하나 입력하세요.>");
        
        Scanner scanner = new Scanner(System.in);
        int tmp = scanner.nextInt();  // console창에서 입력받은 내용을 tmp에 저장;int형만 받을 수 있음
        
        if (input == 0) {
            System.out.println("입력하신 숫자는 0입니다.");
        }
        //if (input == 0) System.out.println("입력하신 숫자는 0입니다.");  // 로도 가능
        
        if (input != 0) {
            System.out.println("입력하신 숫자는 0이 아닙니다.");
            System.out.printf("입력하신 숫자는 %d입니다.", input);
        }
    }
}
```


### 1.2 if-else문
if문의 변형인 if-else문의 구조는 if의 조건식이 참이 아닐경우 else문을 실행시킨다.

```java
if (조건식) {
    // 조건식이 참 일 때 수행될 문장들을 적는다.
} else {
    // 조건식이 거짓 일 때 수행될 문장들을 적는다.
}
```

##### 예제 4-3/ch4/FlowEx3.java
```java
import java.util.*;

class FlowEx3 {
    public static void main(String[] args) {
        System.out.print("숫자를 하나 입력하세요.>");
        
        Scanner scanner = new Scanner(System.in);
        int input = scanner.nextInt();
        
        if (input == 0) {
            System.out.println("입력하신 숫자는 0입니다.");
        } else {
            System.out.println("입력하신 숫자는 0이 아닙니다.");
        }
    }
}
```
뭔가 예제 4-2와 비슷하면서도 짧아진 느낌이 있지 않는가? ~~근데 클린코딩 배우면 글세.... 쓸일 있을까?... if문으로 걍 도배하는게 가독성이 더 좋다하던데~~


### 1.3 if-else if문
if-else문으로 하면 뭔가 좀 아쉽다. 그래서 나온 것이 else if문이다.

```java
if (조건식1) {
    // 조건식1의 연산결과가 참일 때 수행될 문장들을 적는다.
} else if (조건식2) {  // 여러개의 else if를 사용할 수 있다.
    // 조건식2의 연산결과가 참일 때 수행될 문장들을 적는다.
} else {  // 마지막에는 보통 else 블록으로 끝내지만 생략 가능하다.
    // 위의 어느 조건식도 만족하지 않을 때 수행될 문장들을 적는다.
}
```
else if문을 이용하면 학생 점수별로 등급 나누기 같은 것을 쉽게 할 수 있다.

##### 예제 4-4/ch4/FlowEx4.java
```java
import java.util.*;

class FlowEx4 {
    public static void main(String[] args) {
        int score = 0;
        char grade = ' ';

        System.out.println("점수를 입력하세요.>");
        Scanner scanner = new Scanner(System.in);
        score = scanner.nextInt();
        
        if (score >= 90) {
            grade = 'A';
        } else if (score >= 80) {
            grade = 'B';
        } else if (score >= 70) {
            grade = 'C';
        } else {
            grade = 'D';
        }
        System.out.println("당신의 학점은 " + grade + "입니다.");
    }
}
```
처음으로 뭔가 실행되는 걸 만들면 재미있다!! 성취감 겟또  
참고로 복습겸 이 예제를 if문만 사용하는 것으로 한번 바꿔보자! 값이 마구마구 나올 수도 있지만 괜찮다. 작성해보고 왜 그렇게 나오는지 고민해보자


### 1.4 중첩 if문
if문의 블럭 내에 또 다른 if문을 포함시키는 것이 가능한데 이것을 중첩 if문이라고 부르며 중첩의 횟수에는 제한이 없다. ~~가독성을 위해서 2중첩까지만 하고 3중첩이 되면 고민 좀 해보자~~

```java
if (조건식1) {
    // 조건식1의 연산결과가 true일 때 수행될 문장들을 적는다.
    if (조건식2) {
        // 조건식1과 조건식2가 모두 true일 때 수행될 문장들을 적는다.
    } else {
        // 조건식1이 true이고, 조건식2가 false일 때 수행될 문장들을 적는다.
    }
}
```
이전까지는 들여쓰기를 어떻게 했는지 신경 안썼지만 이제부터는 괄호 안에는 한번씩 더 들여쓰도록 신경쓰면서 하자. 안그러면 엄청 곤란하다.

##### 예제 4-5/ch4/FlowEx5.java
```java
import java.util.*;

class FlowEx5 {
    public static void main(String[] args) {
        int score = 0;
        char grade = ' ', opt = '0';

        System.out.println("점수를 입력해주세요.>");
        
        Scanner scanner = new Scanner(System.in);
        score = scanner.nextInt();
        
        System.out.printf("당신의 점수는 %d입니다.%n", score);
        
        if (score >= 90) {
            grade = 'A';
            if (score >= 98) {
                opt = '+';
            } else if (score < 94) {
                opt = '-';
            }
        } else if (score >= 80) {
            grade = 'B';
            if (score >= 88) {
                opt = '+';
            } else if (score < 84) {
                opt = '-';
            }
        } else {
            grade = 'C';
        }
        System.out.printf("당신의 학점은 %c%c입니다.", grade, opt);
    }
}
```
이렇게 학점별로 +, 0, -로 출력 할 수도 있다.


### 1.5 switch문
if문은 조건식의 결과가 참과 거짓이라는 두 가지 밖에 없기 때문에 선택지가 다양할 경우에는 코드가 너무 지저분해지고 별로다.  
이러한 문제점을 해결하기 위해 switch문이 있다. 다만 switch문은 제약조건이 있기 때문에, 경우의 수가 많아도 어쩔 수 없이 if문으로 작성해야 하는 경우가 있다.

```java
switch (조건식) {
    case 값1 :
        // 조건식의 결과가 값1과 같을 경우 수행될 문장들
        break;
    case 값2 :
        // 조건식의 결과가 값2와 같을 경우 수행될 문장들
        break;
    default :
        // 조건식의 결과와 일치하는 case문이 없을 때 수행될 문장들
}
```

##### switch문의 제약조건
1. switch문의 조건식 결과는 정수 또는 문자열이어야 한다.
2. case문의 값은 정수 상수만 가능하며, 중복되지 않아야 한다.

참고로 JDK1.7 이전에는 문자열을 못받았다.

##### 예제 4-6/ch4/FlowEx6.java
```java
import java.util.*;

class FlowEx6 {
    public static void main(String[] args) {
        System.out.println("현재 월을 입력하세요.>");
        
        Scanner scanner = new Scanner(System.in);
        int month = scanner.nextInt();
        
        switch (month) {
          case 3:
          case 4:
          case 5:
              System.out.println("현재의 계절은 봄입니다.");
              break;
          case 6: case 7: case 8:
              System.out.println("현재의 계절은 여름입니다.");
              break;
          case 9: case 10: case 11:
              System.out.println("현재의 계절은 가을입니다.");
              break;
          default:
          case 12: case 1: case 2:
              System.out.println("현재의 계절은 겨울입니다.");
        }
    }
}
```
case문은 한줄에 하나씩 쓰던, 한 줄에 붙여서 쓰던 상관없다. 이 예제를 if문으로 한번 바꿔보는 연습도 해보길 바란다.
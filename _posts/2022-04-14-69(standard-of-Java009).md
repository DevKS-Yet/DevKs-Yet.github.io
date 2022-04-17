---
title: "자바의 정석 9일차"
excerpt: "post"

categories:
- standard-of-java
tags:
- java
- book
---

# Chapter 04 조건문과 반복문(if, switch, for, while statement)

## 2.반복문 - for, while, do-while
반복문이란 어떤 작업을 반복적으로 수행되도록 할 때 사용된다.  
for문이나 while문에 속한 문장은 조건에 따라 한 번도 수행되지 않을 수 있지만 do-while문에 속한 문장은 무조건 최소한 한 번은 수행될 것이 보장된다.

### 2.1 for문
for문은 반복 횟수를 알고 있을 때 적합하다.

```java
for (초기화; 조건식; 증감식) {
    // 수행될 문장
}
```
for문은 위와 같은 구조로 이루어져있다.

###### 초기화
대부분의 for문은 초기화 변수를 하나만 사용하지만 추가적으로 변수를 더하여 사용할 수 있다.

```java
for (int i=1; i<=10; i++) { ... }
for (int i=1, j=0; i<=10; i++) { ... }
```

###### 조건식
중앙에 들어가는 조건식의 값이 참이면 반복을 계속하고 거짓을 하면 반복 중단 및 for문을 벗어난다.

```java
for (int i=1; i<=10; i++) { ... }
```

###### 증감식
반복문을 제어하는 변수의 값을 증가 또는 감소시키는 식이다. 주로 ++, --를 사용하지만 +=, -=, *=, /=, %=도 사용이 가능하다.  
또한 증감식도 ','를 이용해서 두 문장 이상을 하나로 연결해서 쓸 수 있다.

```java
for (int i=1, j=10; i<=10; i++, j--) { ... }
```

##### 예제 4-12/ch4/FlowEx12.java
```java
class FlowEx12 {
    public static void main(String[] args) {
        for (int i=1; i<=5; i++) {
            System.out.println(i);
        }
        for (int i=1; i<=5; i++) {
            System.out.print(i);
        }
        System.out.println();
    }
}
```
위 예제를 통해서 초기화 변수가 1부터 시작하여 5까지만 반복하는 것을 확인할 수 있다.

##### 예제 4-13/ch4/FlowEx13.java
```java
class FlowEx13 {
    public static void main(String[] args) {
        int sum = 0;
        for (int i=1; i<=10; i++) {
            sum += i;
            System.out.printf("1부터 %2d 까지의 합: %2d%n", i, sum);
        }
    }
}
```
위 예제를 통해서 1부터 10까지의 합을 구할 수 있다. 참고로 `sum += i` 는 `sum = sum + i`이다.

##### 예제 4-14/ch4/FlowEx14.java
```java
class FlowEx14 {
    public static void main(String[] args) {
        for(int i=1, j=10; i<=10; i++, j--) {
            System.out.printf("%d \t %d%n", i, j);
        }
    }
}
```
for문에 두 개의 변수를 사용한 예제이다. 자주 쓸일은 없지만 틀린 문법은 아니니 나중에 보더라도 '에거 에러 발생 아닌가요?'는 하지말자

##### 예제 4-15/ch4/FlowEx15.java
```java
class FlowEx15 {
    public static void main(String[] args) {
        System.out.println("i \t 2*i \t 2*i-1 \t i*i \t 11-i \t i%3 \t i/3");
        System.out.println("----------------------------------------------");
        
        for (int i=1; i<=10; i++) {
            System.out.printf("%d \t %d \t %d \t %d \t %d \t %d \t %d\n", i, 2*i, 2*i-1, i*i, 11-i, i%3, i/3);
        }
    }
}
```
이 예제는 그냥 넘어가도 괜찮다고 생각한다.

###### 중첩 for문
조건문에서도 중첩 if문이나 switch문이 있었듯이 반복문도 중첩이 가능하다.  
기본적으로 for문을 한번만 사용해서 출력했던 것들 중첩 for문으로 바꿔보자

##### 예제 4-16/ch4/FlowEx16.java
```java
class FlowEx16 {
    public static void main(String[] args) {
        for (int i=1; i<=5; i++) {
            for (int j=1; j<=10; j++) {
                System.out.print("*");
            }
            System.out.println();
        }
    }
}
```
위 예제를 실행하면 굳이 이중 for문을 써야하나 싶다. 오히려 코드가 더 지저분한 느낌이다.  
하지만 조건문와 반복문을 배우고나서 필수적으로 찍는다는 삼각형 모양의 별을 출력할려면 어떻게 해야할까?

##### 예제 4-17/ch4/FlowEx17.java
```java
import java.util.*;

class FlowEx17 {
    public static void main(String[] args) {
        int num = 0;

        System.out.print("*을 출력할 라인의 수를 입력하세요.>");
        
        Scanner scanner = new Scanner(System.in);
        String tmp = scanner.nextLine();
        num = Integer.parseInt(tmp);
        
        for (int i=0; i<num; i++) {
            for (int j=0; j<=i; j++) {
                System.out.print("*");
            }
            System.out.println();
        }
    }
}
```
위와 비슷한 개념으로 좌우 또는 상하 대칭되는 삼각형이나 마름모(또는 정사각형)도 만들 수 있다. 너무 많은 시간을 할애할 필요는 없고 30분정도만 생각해보자

##### 예제 4-18/ch4/FlowEx18.java
```java
class FlowEx18 {
    public static void main(String[] args) {
        for (int i=2; i<=9; i++) {
            for (int j=1; j<=9; j++) {
                System.out.printf("%d x %d = %d%n", i, j, i*j);
            }
        }
    }
}
```
위 예제는 구구단을 출력한 것이다. 이렇게 출력할 시에는 가독성이 좋아보이는 않아보인다. 그렇다면 우리가 평상시 알고있는 구구단 종이처럼 출력도 해보자

```
1*1=1 2*1=2 3*1=3 4*1=4 ....
1*2=2 2*2=4 3*2=6 4*2=8 ....
.............
```

##### 예제 4-19/ch4/FlowEx19.java
```java
class FlowEx19 {
    public static void main(String[] args) {
        for (int i=1; i<=3; i++) {
            for (int j=1; j<=3; j++) {
                for (int k = 1; j<=3; k++) {
                    System.out.println("" + i + k + j);
                }
            }
        }
    }
}
```
3중첩 for문이다. 각 for문당 3번씩 반복하고 있음으로 총 출력 횟수는 3*3*3=27개 이다.

##### 예제 4-20/ch4/FlowEx20.java
```java
class FlowEx20 {
    public static void main(String[] args) {
        for (int i=1; i<=5; i++) {
            for (int j=1; j<=5; j++) {
                System.out.printf("[%d, %d]", i, j);
            }
            System.out.println();
        }
    }
}
```
위 예제를 보면 이과 학생이라면 좌표나 벡터가 생각날 것이고 문과 학생이라면 엑셀표가 생각나지 않을까 싶다....  
지금까지 이중 for문으로 2차원적으로 출력을 했지만 이번 예제를 통해서 확실하게 확인할 수 있다.

##### 예제 4-21/ch4/FlowEx21.java
```java
class FlowEx21 {
    public static void main(String[] args) {
        for (int i=1; i<=5; i++) {
            for (int j=1; j<=5; j++) {
                if (i==j) {
                    System.out.printf("[%d, %d]", i, j);
                } else {
                    System.out.printf("%5c", ' ');  // 5개의 자릿수만큼 ' '을 대입
                }
            }
            System.out.println();
        }
    }
}
```
`i==j`가 성립 될 때만 출력되도록 하고 아닐 경우에는 공백을 채워넣도록 하였다.  
위 예제를 응용한다면 예제 4-17에서 말한 좌우 또는 상하 대칭 삼각형이나 마름모형도 출력하기가 조금 더 수월하다.

###### 향상된 for문(enhanced for statement)
JDK 1.5부터 배열과 컬렉션에 저장된 요소에 접근할 때 기존보다 편리한 방법으로 처리할 수 있도록 for문의 새로운 문법이 추가되었다.

```java
for ( 타입 변수명 : 배열 또는 컬렉션) {
    // 반복할 문장
}
```
위의 문장만 봐서는 솔직히 1도 모르겠다. 배열과 컬렉션도 안배운 시점에서 이게 뭔가 싶다. 그러므로 이런게 있다 정도로만 넘어가고 사용하기가 너무 어렵다싶으면 평상시 사용한 for문으로 사용해도 된다.

##### 예제 4-22/ch4/FlowEx2.java
```java
class FlowEx22 {
    public static void main(String[] args) {
        int[] arr = {10, 20, 30, 40, 50};
        int sum = 0;
        
        for (int i=0; i<arr.length; i++) {
            System.out.printf("%d ", arr[i]);
        }
        System.out.println();
        
        for (int tmp : arr) {
            System.out.printf("%d ", tmp);
            sum += tmp;
        }
        System.out.println();
        System.out.println("sum = " + sum);
    }
}
```
`int[] arr`이라는 것은 배열이다. 아직 진도를 나가지는 않았지만 궁금하다면 해당 링크를 참고해주길 바란다[링크](https://devks-yet.github.io/post/71(data-structure2)/).
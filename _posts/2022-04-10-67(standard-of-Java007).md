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

## 5. 논리 연산자
'x가 4보다 작다'라는 조건은 비교연산자를 써서 'x < 4'와 같이 표현할 수 있지만 'x가 4보다 작거나 또는 10보다 크다'와 같은 두 개의 조건이 결합된 경우에는 비교 연산자만 사용해서 풀 수 없다.  
이때 사용하는 것이 'AND' 또는 'OR'로 연결하는 논리 연산자다.


### 5.1 논리 연산자 - &&, ||,  !
논리 연산자의 연산결과는 항상 `boolean`형으로 나오며 피연산자에 따른 결과는 아래와 같다.

| x | y | x &#124;&#124; y | x &amp;&amp; y |
|:---:|:---:|:---:|:---:|
| true | true | true | true |
| true | false | true | false |
| false | true | true | false |
| false | false | false | false |

- &#124;&#124; (OR결합) - 피연산자 중 어느 한 쪽만 true이면 true를 결과로 얻는다.
- &amp;&amp; (AND결합) - 피연산자 양쪽 모두 true이어야 true를 결과로 얻는다.

##### 예제 3-24/ch3/OperatorEx24.java
```java
class OperatorEx24 {
    public static void main(String[] args) {
        int x = 0;
        char ch = ' ';
        
        x = 15;
        System.out.printf("x = %2d, 10 < x && x < 20 = %b%n", x, 10 < x && x < 20);
        x = 6;
        System.out.printf("x = %2d, x%%2==0 || x%%3==0 && x%%6!=0 = %b%n", x, x%2==0 || x%3==0 &&x%6 != 0);
        System.out.printf("x = %2d, (x%%2==0 || x%%3==0) && x%%6!=0 = %b%n", x, (x%2==0 || x%3==0) &&x%6 != 0);
        ch = '1';
        System.out.printf("ch='%c', '0' <= ch && ch <= '9' =%b%n", ch, '0' <= ch && ch <= '9');
        ch = 'a';
        System.out.printf("ch='%c', 'a' <= ch && ch <= 'z' =%b%n", ch, 'a' <= ch && ch <= 'z');
        ch = 'A';
        System.out.printf("ch='%c', 'A' <= ch && ch <= 'Z' =%b%n", ch, 'A' <= ch && ch <= 'Z');
        ch = 'q';
        System.out.printf("ch='%c', ch == 'q' || ch == 'Q' =%b%n", ch, ch == 'q' || ch == 'Q');
    }
}
```
위 예제는 실행하기 전에 결과값을 한번 예상하고 실행하자.

##### 예제 3-25/ch3/OperatorEx25.java
```java
import java.util.*;

class OperatorEx25 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        char ch = ' ';

        System.out.printf("문자를 하나 입력하세요.>");
        
        String input = scanner.nextLine();
        ch = input.charAt(0);
        
        if ('0' <= ch && ch <= '9') {
            System.out.printf("입력하신 문자는 숫자입니다.%n");
        }
        if (('a' <= ch && ch <= 'z') || ('A' <= ch && ch <= 'Z')) {
            System.out.printf("입력하신 문자는 영문자입니다.%n");
        }
    }
}
```
if문 관련해서는 뒤에 배움으로 가볍게 if문 괄호 안의 값이 true이면 실행되는 것이고 false라면 실행을 안한다 정도까지만 알자.

###### 효율적인 연산(short circuit evaluation)
OR연산일 경우 두 피연산자 중 한 쪽만 '참'이어도 전체 연산결과가 '참'이므로 좌측 피연산자가 'true(참)'이면, 우측 피연산자의 값은 평가하지 않는다.

AND연산일 경우도 마찬가지이다. 좌측 피연산자가 'false(거짓)'이라면 우측 피연산자의 값은 평가하지 않는다.

##### 예제 3-26/ch3/OperatorEx26.java
```java
class OperatorEx26 {
    public static void main(String[] args) {
        int a = 5;
        int b = 0;

        System.out.printf("a = %d, b = %d%n", a, b);
        System.out.printf("a != 0 || ++b != 0 = %b%n", a != 0 || ++b != 0);
        System.out.printf("a = %d, b = %d%n", a, b);
        System.out.printf("a == 0 && ++b != 0 = %b%n", a ==0 && ++b != 0);
        System.out.printf("a = %d, b = %d%n", a, b);
    }
}
```
위 예제는 효율적인 연산을 하는지 확인하는 예제이다. ~~사실 그렇게까지 필요는 없다....~~

###### 논리 부정 연산자 !
부정 연산자(!)는 피연산자가 true이면 false로 false이면 true로 결과를 반환한다. 수학과 친구들은 집합론에서 Not을 생각하면 된다. ~~정작 수학에서는 !를 유일하다로 사용하지만.....~~

| x | !x |
|:---:|:---:|
| true | false |
| false | true |

##### 예제 3-27/ch3/OperatorEx27.java
```java
class OperatorEx27 {
    public static void main(String[] args) {
        boolean b = true;
        chjar ch = 'C';

        System.out.printf("b = %b%n", b);
        System.out.printf("!b = %b%n", !b);
        System.out.printf("!!b = %b%n", !!b);
        System.out.printf("!!!b = %b%n", !!!b);
        System.out.println();

        System.out.printf("ch = %c%n", ch);
        System.out.printf("ch < 'a' || ch > 'z' = %b%n", ch < 'a' || ch > 'z');
        System.out.printf("!(ch < 'a' && ch > 'z') = %b%n", !(ch < 'a' && ch > 'z'));
        System.out.printf("ch < 'a' && ch > 'z' = %b%n", ch < 'a' && ch > 'z');
    }
}
```


### 5.2 비트 연산자 & | ^ ~ << >>
비트 연산자는 피연산자를 비트단위로 논리 연산을 한다. 이부분은 웹프로그래밍을 하면서 그렇게 사용할 일이 없다.

&#124;(OR연산자) - 피연산자 중 한 쪽의 값이 1이면, 1을 결과로 얻는다. 그 외에는 0을 얻는다.
&amps;(AND연산자) - 피연산자 양 쪽이 모두 1이어야만 1을 결과로 얻는다. 그 외에는 0을 얻는다.
^(XOR연산자) - 피연산자의 값이 서로 다를 때만 1을 결과로 얻는다. 같을 때는 0을 얻는다.

| x | y | x &#124; y | x &amps; y | x ^ y |
|:---:|:---:|:---:|:---:|:---:|
| 1 | 1 | 1 | 1 | 0 |
| 1 | 0 | 1 | 0 | 1 |
| 0 | 1 | 1 | 0 | 1 |
| 0 | 0 | 0 | 0 | 0 |

##### 예제 3-28/ch3/OperatorEx28.java
```java
class OperatorEx28 {
    public static void main(String[] args) {
        int x = 0xAB, y = 0xF;

        System.out.printf("x = %#X \t\t %s%n", x, toBinaryString(x));
        System.out.printf("y = %#X \t\t %s%n", y, toBinaryString(y));
        System.out.printf("%#X | %#X = %#X \t\t %s%n", x, y, x | y, toBinaryString(x | y));
        System.out.printf("%#X & %#X = %#X \t\t %s%n", x, y, x & y, toBinaryString(x & y));
        System.out.printf("%#X ^ %#X = %#X \t\t %s%n", x, y, x ^ y, toBinaryString(x ^ y));
        System.out.printf("%#X ^ %#X ^ %#X = %#X \t\t %s%n", x, y, x ^ y ^ y, toBinaryString(x ^ y ^ y));
    }
    static String toBinaryString(int x) {
        String zero = "00000000000000000000000000000000";
        String tmp = zero + Integer.toBinaryString(x);
        return tmp.substring(tmp.length()-32);
    }
}
```

###### 비트 전환 연산자 ~
비트 연산자에도 논리 연산자에서 부정 연산자가 있었듯이 전환 연산자가 있다.

| x | ~x |
|:---:|:---:|
| 1 | 0 |
| 0 | 1 |

##### 예제 3-29/ch3/OperatorEx29.java
```java
class OperatorEx29 {
    public static void main(String[] args) {
        byte p = 10;
        byte n = -10;

        System.out.printf("p = %d \t%s%n", p, toBinaryString(p));
        System.out.printf("~p = %d \t%s%n", ~p, toBinaryString(~p));
        System.out.printf("~p+1 = %d \t%s%n", ~p+1, toBinaryString(~p+1));
        System.out.printf("~~p = %d \t%s%n", ~~p, toBinaryString(~~p));
        System.out.println();
        System.out.printf("n = %d%n", n);
        System.out.printf("~(n-1) = %d%n", ~(n-1));
    }
    static String toBinaryString(int x) {
        String zero = "00000000000000000000000000000000";
        String tmp = zero + Integer.toBinaryString(x);
        return tmp.substring(tmp.length()-32);
    }
}
```

###### 쉬프트 연산자 << >>
피연산자의 각 자리(2진수로 표현했을 때)를 '오른쪽(&gt;&gt;)' 또는 '왼쪽(&lt;&lt;)'으로 이동한다고 해서 '쉬프트 연산자'이다.

해당 연산자는 나눗셈이나 곱셈 연산자를 사용하는 것보다 더 빠르나 프로그램을 개발할 때 코드의 가독성도 중요하다. 그렇기에 빠른 실행속도가 요구되는 곳이 아닌이상 쓸 일 없다.

##### 예제 3-30/ch3/OperatorEx30.java
```java
class OperatorEx30 {
    static String toBinaryString(int x) {
        String zero = "00000000000000000000000000000000";
        String tmp = zero + Integer.toBinaryString(x);
        return tmp.substring(tmp.length()-32);
    }
    public static void main(String[] args) {
        int dec = 8;
        System.out.printf("%d >> %d = %4d \t%s%n", dec, 0, dec >> 0, toBinaryString(dec >> 0));
        System.out.printf("%d >> %d = %4d \t%s%n", dec, 1, dec >> 1, toBinaryString(dec >> 1));
        System.out.printf("%d >> %d = %4d \t%s%n", dec, 2, dec >> 2, toBinaryString(dec >> 2));
        System.out.printf("%d << %d = %4d \t%s%n", dec, 0, dec << 0, toBinaryString(dec << 0));
        System.out.printf("%d << %d = %4d \t%s%n", dec, 0, dec << 1, toBinaryString(dec << 1));
        System.out.printf("%d << %d = %4d \t%s%n", dec, 0, dec << 2, toBinaryString(dec << 2));
        System.out.println();
        
        dec = -8;
        System.out.printf("%d >> %d = %4d \t%s%n", dec, 0, dec >> 0, toBinaryString(dec >> 0));
        System.out.printf("%d >> %d = %4d \t%s%n", dec, 1, dec >> 1, toBinaryString(dec >> 1));
        System.out.printf("%d >> %d = %4d \t%s%n", dec, 2, dec >> 2, toBinaryString(dec >> 2));
        System.out.printf("%d << %d = %4d \t%s%n", dec, 0, dec << 0, toBinaryString(dec << 0));
        System.out.printf("%d << %d = %4d \t%s%n", dec, 0, dec << 1, toBinaryString(dec << 1));
        System.out.printf("%d << %d = %4d \t%s%n", dec, 0, dec << 2, toBinaryString(dec << 2));
        System.out.println();
        
        dec = 8;
        System.out.printf("%d >> %2d = %4d \t%s%n", dec, 0, dec >> 0, toBinaryString(dec >> 0));
        System.out.printf("%d >> %2d = %4d \t%s%n", dec, 32, dec >> 32, toBinaryString(dec >> 32));
    }
}
```

##### 예제 3-31/ch3/OperatorEx31.java
```java
class OperatorEx31 {
    public static void main(String[] args) {
        int dec = 1234;
        int hex = 0xABCD;
        int mask = 0xF;

        System.out.printf("hex = %X%n", hex);
        System.out.printf("%X%n", hex & mask);
        
        hex = hex >> 4;
        System.out.printf("%X%n", hex & mask);
        
        hex = hex >> 4;
        System.out.printf("%X%n", hex & mask);
        
        hex = hex >> 4;
        System.out.printf("%X%n", hex & mask);
    }
}
```


## 6. 그 외의 연산자

### 6.1 조건 연산자 ? :
조건 연산자는 조건식, 식1, 식2 모두 세 개의 피연산자를 필요로 하는 삼항 연산자이며, 삼항 연산자는 조건 연산자 하나뿐이다.

예) `result = (x > y ) ? x : y ;`  
이렇게 적으면 x가 y보다 크면 x를 저장하고 x가 y보다 작다면 y를 저장한다.  
if문으로 적는다면 아래와 같다.

```java
if (x > y) {
    result = x;
  } else {
    result = y;
  }
```

##### 예제 3-32/ch3/OperatorEx32.java
```java
class OperatorEx32 {
    public static void main(String[] args) {
        int x, y, z;
        int absX, absY, absZ;
        char signX, signY, signZ;
        
        x = 10;
        y = -5;
        z = 0;
        
        absX = x >= 0 ? x : -x;
        absY = y >= 0 ? y : -y;
        absZ = z >= 0 ? z : -z;
        
        signX = x > 0 ? '+' : (x == 0 ? ' ' : ' - ');
        signY = y > 0 ? '+' : (y == 0 ? ' ' : ' - ');
        signZ = z > 0 ? '+' : (z == 0 ? ' ' : ' - ');

        System.out.printf("x = %c%d%n", signX, absX);
        System.out.printf("y = %c%d%n", signY, absY);
        System.out.printf("z = %c%d%n", signZ, absZ);
    }
}
```


### 6.2 대입 연산자 = op=
대입 연산자는 변수와 같은 저장공간에 값 또는 수식의 연산결과를 저장하는데 사용된다.

###### lvalue와 rvalue
대입 연산자의 왼쪽 피연산자를 'lvalue(left value)'라 하고, 오른쪽 피연산자는 'rvalue(right value)'라고 한다.  
rvalue는 변수뿐만 아니라 식이나 상수 등 모두 가능한 반면, lvalue는 리터럴이나 상수같이 값을 저장할 수 없는 것들이 불가능하다.

###### 복합 대입 연산자
대입 연산자에 다른 연산자(op)를 결합하여 'op='으로 사용할 수 있다.

| op= | = |
|:---:|:---:|
| i += 3; | i = i + 3; |
| i -= 3; | i = i - 3; |
| i *= 3; | i = i * 3; |
| i /= 3; | i = i / 3; |
| i %= 3; | i = i % 3; |
| i <<= 3; | i = i << 3; |
| i >>= 3; | i = i >> 3; |
| i &= 3; | i = i & 3; |
| i ^= 3; | i = i ^ 3; |
| i &#124;= 3; | i = i &#124; 3; |
| i *= 10 + j | i = i * (10+j); |


> 복합 대입 연산자를 마무리로 chapter3 연산자가 끝났다. 많이 생략된 부분도 있으니 읽다가 이해가 안가거나 뭔가 아쉬운 점은 댓글로 남기거나 스스로 추가적으로 공부를 더 하면 좋겠다.  
> 이 책을 읽기 시작한 이유는 객체지향 프로그래밍과 람다와 스트림 사용법 때문에 읽기 시작한 것임으로 그 전 내용들은 매우매우 부실할 수 있다.
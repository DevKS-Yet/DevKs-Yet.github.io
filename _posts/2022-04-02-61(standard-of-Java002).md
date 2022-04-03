---
title: "자바의 정석 2일차"
excerpt: "post"

categories:
- standard-of-java
tags:
- java
- book
---

# Chapter 02 변수(Variable)

## 1. 변수(Variable)
결국에 프로그래밍이라는 것은 데이터를 잘 다뤄야하는 것이다. 그렇기 위해서는 변수에 대해서 알아본다.

### 1.1 변수(variable)란?
수학에서는 '변수'란 '변하는 수'로 정의하지만 프로그래밍 언어에서는 값을 저장할 수 있는 메모리상의 공간을 의미한다(수학과라서 이 책을 읽기 전까지 변하는 수로 알고있었다). 물론 이 공간에 저장된 값이 변경이 불가능하지는 않다. 변경 될 수 있기에 변수라는 이름이 붙여진 것이다.

### 1.2 변수의 선언과 초기화
**"변수 초기화란, 변수를 사용하지 전에 처음으로 값을 저장하는 것"**
- 선언방법
```java
int age;  // age라는 이름의 변수를 선언
```
`int`는 각종 변수 타입으로 변경 가능하며 변수의 이름은 예약어를 제외하고 사용자 마음대로 만들 수 있다.
- 변수의 초기화
```java
int a;  // a, b라는 변수는 초기화가 안된 상태. 전역변수일 경우에는 컴파일 도중 알아서 int의 기본값인 0을 대입
int b;
int x = 0;  // x, y라는 변수에 0으로 초기화
int y = 0;
```
  변수의 종류에 따라서 변수의 초기화를 생략할 수 있는 경우도 있지만 적절한 값으로 항상 초기화 하는 것이 좋다.

##### 예제 2-1/ch2/VarEx1.java
변수 초기화
```java
class VarEx1 {
    public static void main (String[] args) {
        int year = 0;
        int age = 14;
      System.out.println(year);
      System.out.println(age);
        
        year = age + 2000;
        age = age + 1;
      System.out.println(year);
      System.out.println(age);
    }
}
```

##### 예제 2-2/ch2/VarEx2.java
두 변수의 값 교환하기
```java
class VarEx2 {
    public static void main(String[] args) {
        int x = 10, y = 20;  // 동일한 타입의 변수는 생략해서 이렇게 적을 수도 있다.
        int tmp = 0;

      System.out.println("x: " + x + "\ny: " + y);
      
        tmp = x;
        x = y;
        y = tmp;

      System.out.println("x: " + x + "\ny: " + y);
    }
}
```

### 1.3 변수의 명명규칙
개발자들이 가장 어렵다고 하는 변수 이름을 짓기 전에 지켜야하는 규칙이다.
1. 대소문자가 구분되며 길이에 제한이 없다.
   - `True`와 `true`는 서로 다른 것으로 간주된다.
2. 예약어는 사용해서는 안 된다.
   - `true`는 예약어라서 사용할 수 없지만, `True`는 가능하다(하지만 추천하지는 않는다).
3. 숫자로 시작해서는 안 된다.
   - `top10`은 허용하지만, `7up`은 허영되지 않는다.
4. 특수문자는 `_`와 `$`만을 허용한다.
   - `$harp`은 허용되지만, `S#arp`은 허용되지 않는다.

위 사항들은 지켜지지 않을 시 시스템적으로 에러를 발생한다. 아래 규칙은 필수는 아니지만 권장하는 규칙들이다.
1. 클래스 이름의 첫 글자는 항상 대문자로 한다.
   - 변수와 메서드의 이름의 첫 글자는 항상 소문자로 한다.
2. 여러 단어로 이루어진 이름은 단어의 첫 글자를 대문자로 한다.
   - `lastIndexOf`, `StringBuffer`
3. 상수의 이름은 모두 대문자로 한다. 여러 단어로 이루어진 경우 `_`로 구분한다.
   - `PI`, `MAX_NUMBER`

회사 또는 프로젝트팀마다 권장 규칙이 살짝 다를 수는 있으나 왠만하면 권장 규칙은 동일하게 간다.


## 2. 변수의 타입
값의 종류는 '문자와 숫자'로 나눌 수 있으면 숫자도 '정수와 실수'로 나눌 수 있다.  
이러한 값의 종류에 따라 값이 저장될 공간의 크기와 저장형식을 정의한 것이 자료형(data type)이다. 자료형에는 문자형(char), 정수형(byte, short, int, long), 실수형(float, double) 등이 있으며 변수를 선언할 때는 저장하려는 값의 특성을 고려하여 가장 알맞은 자료형을 변수의 타입으로 선택하면 된다.

자료형은 크게 `기본형`과 `참조형`으로 나뉜다. 기본형은 실제 값을 저장하는 것이고 참조형은 주소를 값으로 갖는 것이다.  
`기본형`의 상세부분에 대해서는 추후에 표로 보여주는게 나은 것 같아서 해당 부분은 제외하였다.

앞서 변수 선언 방법때 사용했던 것이 기본형 변수 선언이였기에 이번에는 참조형 변수를 선언하는 방법에 대해서 적겠다.
- 참조형 변수 선언
```java
String sentence = new String();  // String이라는 객체를 생성해서 해당 객체의 주소를 sentence에 저장
```
만약 코드를 조금 배우셨던 분이라면 이상하다라는걸 느끼셨을 수도 있다.  
String은 `String sentence = "Hello World";`으로 선언 및 초기화까지도 가능하다. 하지만 이것은 자바에서 자주 사용하는 String이 참조형이더라도 기본형처럼 기능을 더해준 것이다. String은 절대로 기본형이 아니다.

### 2.1 기본형(primitive type)
기본형에는 총 8개의 자료형이 있으며 논리형, 문자형, 정수형, 실수형으로 구분된다.

| 종류 | 자료형 | 크기(byte) | 표현 범위 | 접미사 | 설명 |
|:---:|:---|:---:|:---|:---:|:---:|
| 논리형 | boolean | 1 | true, false | 없음 | 조건식과 논리적 계산에 사용된다. |
| 문자형 | char | 2 | '\u0000' ~ '\uffff' (0 ~ (2^16)-1) | 없음 | 문자를 저장하는데 사용되며, 변수에 하나의 문자만 저장할 수 있다. |
| 정수형 | byte | 1 | -(2^7) ~ (2^7)-1 | 없음 | 정수 데이터 중 이진 데이터를 다룰 때 사용된다. |
| 정수형 | short | 2 | -(2^15) ~ (2^15)-1 | 없음 | C언어와의 호환을 위해서 추가되었다. |
| 정수형 | int | 4 | -(2^31) ~ (2^31)-1 | 없음 | 정수를 저장하는데 주로 사용된다. |
| 정수형 | long | 8 | -(2^63) ~ (2^63)-1 | L | int 범위를 넘는 정수를 담을 때 사용된다. |
| 실수형 | float | 4 | 1.4E-45 ~ 3.4E38 | f | 실수를 저장하는데 사용된다. |
| 실수형 | double | 8 | 4.9E-324 ~ 1.8E308 | d | 실수를 저장하는데 주로 사용된다. |

- `char`은 문자를 내부적으로 정수로 저장하기 때문에 정수형 또는 실수형과 연산도 가능하다. `boolean`만 다른 기본형들과 연산이 불가능하다.
- 정수형 중에서는 `int`형이 기본 자료형이다.
- 실수형 중에서는 `double`형이 기본 자료형이다.


실수형은 정수형과 저장형식이 달라서 같은 크기(byte)라도 훨씬 큰 값을 표현할 수 있으나 오차가 발생할 수 있다는 단점이 있다. 그래서 정밀도가 중요하며 정밀도가 높을수록 발생할 수 있는 오차의 범위가 줄어든다.

| 자료형 | 정밀도 | 크기(byte) |
|:---:|:---:|:---:|
| float | 7자리 | 4 |
| double | 15자리 | 8 |


### 2.2 상수와 리터럴(constant &amp; literal)

###### 상수(constant)
상수도 변수와 같이 값을 저장할 수 있는 공간이지만 다른 점은 한번 값을 저장하면 다른 값으로 변경할 수 없다. 선언은 다음과 같다.
```java
final int MAX_SPEED;  // 에러. 상수는 선언과 동시에 초기화해야함
final int MAX_VALUE = 100;  // 정상. 상수 MAX_SPEED를 선언 & 초기화
MAX_VALUE = 200;  // 에러. 상수의 값은 변경될 수 없음.
```

###### 리터럴(literal)
상수와 리터럴이라는 것이 개념이 좀 많이 헷갈릴 수 있다. ~~필자만 그랬을 수도 있다.~~  
프로그래밍에서는 상수를 '값을 한 번 저장하면 변경할 수 없는 저장공간'으로 정의하였기에 상수 대신 리터럴이라는 용어를 사용한다.  
단어의 뜻들은 다음과 같다.

| 이름 | 설명 |
|:---|:---|
| 변수(variable) | 하나의 값을 저장하기 위한 공간 |
| 상수(constant) | 값을 한번만 저장할 수 있는 공간 |
| 리터럴(literal) | 그 자체로 값을 의미하는 것 |

아직도 헷갈린다면 원래 우리가 알고 있는 `1`, `132`, `3.254`, `A` 같은 것들이 상수이지만 프로그래밍에서는 상수가 다른 단어로 사용되서 이런 것들을 리터럴이라고 한다.

###### 상수가 필요한 이유
굳이 상수(constant)를 쓰는 이유가 뭘까 라는 생각이 들 수 있다. 변수명을 보면 알수 있을 것이고 해당 값을 고정시키는게 좋은건가 라는 고민이 들 수도 있다.  
필자도 학원에서 프로젝트를 진행할때에는 상수를 사용한 적이 없다. 소규모 프로젝트이기도 했지만 인원들 또한 필요성을 느끼지 못했기 때문이다. 그렇기에 지금 당장 상수를 쓰라고 말하고 싶지는 않다. 다만 취업 후 회사에 입사를 한 후에는 꼭 프로젝트의 규모를 경험해보길 바란다. 그렇다면 상수를 왜 사용하는지 또는 사용할 수 밖에 없는 이유를 조금이나마 체감되게 느낄 수 있다.

###### 문자 리터럴과 문자열 리터럴
문자 리터럴은 문자 하나, 문자열 리터럴은 문자 하나 이상이라고 생각하면 된다(그냥 구분을 `''`로 감싸는지 아니면 `""`로 감싸는지 여부를 따지는게 더 편할듯?).
```java
char ch = 'C';  // char 에는 'Cho' 이렇게 저장할 수 없다. 문자 하나만 저장 가능
String name = "Cho"  // String은 사실 하나만 저장도 가능하지만 char처럼 연산이 가능하지는 않다.
```

```java
String str = "";  // 정상. 내용이 없는 빈 문자열(null과는 다름)
char ch = '';  // 에러. ''안에 반드시 하나의 문자가 필요
char ch = ' ';  // 정상. 공백 문자로 변수 ch 초기화
```

이전에도 언급을 했지만 원래 String은 클래스이므로 객체를 생성하는 연산자 new를 사용해야하지만 Java에서 특별히 위와 같은 표현도 가능하도록 하였다.  
또한 덧셈 연산자를 통해 문자열을 결합할 수 있다.
```java
String firstName = KyuSang;
String lastName = new String("Cho");
String fullName = firstName + lastName;
```

또는 숫자형과 더할 때에는 숫자형이 문자열로 바뀌면서 해당 문자열과 결합된다.
```
문자열 + any type -> 문자열 + 문자열 -> 문자열
any type + 문자열 -> 문자열 + 문자열 -> 문자열
```

##### 예제 2-3/ch2/StringEx.java
```java
class StringEx {
    public static void main(String[] args) {
        String name = "Ja" + "va";
        String str = name + 8.0;
        
        System.out.println(name);
        System.out.println(str);
        System.out.println(7 + " ");
        System.out.println(" " + 7);
        System.out.println(7 + "");
        System.out.println("" + 7);
        System.out.println("" + "");
        System.out.println(7 + 7 + "");
        System.out.println("" + 7 + 7);
    }
}
```
위 예제를 꼭 실행해보고 변경해서도 출력해보길 바란다.

### 2.3 형식화된 출력 - printf()
println은 다른 형식으로 값을 출력할 수 없었다. 하지만 printf를 통해서 10진수를 16진수나 8진수로 자동적으로 변환을 해서 출력하도록 가능하다.  
지시자는 다음과 같다.

| 지시자 | 설명 |
|:---|:---|
| %n | 줄바꿈 |
| %b | boolean 형식으로 출력 |
| %d | 10진(decimal) 정수의 형식으로 출력 |
| %o | 8진(octal) 정수의 형식으로 출력 |
| %x, %X | 16진(hexa-decimal) 정수의 형식으로 출력 |
| %f | 부동 소수점(floating-point)의 형식으로 출력 |
| %e, %E | 지수(exponent) 표현식의 형식으로 출력 |
| %c | 문자(character)로 출력 |
| %s | 문자열(string)로 출력 |

##### 예제 2-4/ch2/PrintfEx1.java
```java
class PrintfEx1 {
    public static void main(String[] args) {
        byte b = 1;
        short s = 2;
        char c = 'A';
        
        int finger = 10;
        long big = 100_000_000_000L;  // Java1.7 이상부터는 _를 넣어도 인식이 된다. 한국은 왜 3개씩 ,를 찍지?... 4개씩 찍어야하는데
        long hex = 0xFFFF_FFFF_FFFF_FFFFL;
        
        int octNum = 010;  // 10
        int hexNum = 0x10;  // 16
        int binNum = 0b10;  // 2

        System.out.println("b=%d%n", b);
        System.out.println("s=%d%n", s);
        System.out.println("c=%c, %d %n", c, (int)c);
        System.out.println("finger=[%5d]%n", finger);
        System.out.println("finger=[%-5d]%n", finger);
        System.out.println("finger=[%05d]%n", finger);
        System.out.println("big=%d%n", big);
        System.out.println("hex=%d%n", hex);
        System.out.println("octNum=%o, %d%n", octNum, octNum);
        System.out.println("hexNum=%o, %d%n", hexNum, hexNum);
        System.out.println("binNum=%s, %d%n", Integer.toBinaryString(binNum));
    }
}
```

##### 예제 2-5/ch2/PrintfEx2.java
```java
class PrintfEx2 {
    public static void main(String[] args) {
        String url = "github.com/DevKs-Yet";
        
        float f1 = .10f;
        float f2 = 1e1f;
        float f3 = 3.14e3f;
        double d = 1.23456789;

        System.out.printf("f1=%f, %e, %g%n", f1, f1, f1);
        System.out.printf("f2=%f, %e, %g%n", f2, f2, f2);
        System.out.printf("f3=%f, %e, %g%n", f3, f3, f3);
        
        System.out.printf("d=%f%n", d);
        System.out.printf("d=%14.10f%n", d);
        
        System.out.printf("[12345678901234567890]%n");
        System.out.printf("[%s]%n", url);
        System.out.printf("[%20s]%n", url);
        System.out.printf("[%-20s]%n", url);
        System.out.printf("[%.10s]%n", url);
    }
}
```
숫자를 바꿔바면서 원하는 출력공간을 만들어보도록 하자.

### 2.4 화면에서 입력받기 - Scanner
지금까지 출력만 해왔는데 입력도 한번 해보자

##### 예제 2-6/ch2/ScannerEx.java
```java
import java.util.*;  // Scanner 클래스를 사용하기 위해 추가

class ScannerEx {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);  // Scanner 클래스 객체 생성
        
        System.out.print("두 자리 정수를 하나 입력해주세요: ");
        String input = scanner.nextLine();  // Scanner(System.in)의 메소드 중 하나인 nextLine()을 호출
        int num = Integer.parseInt(input);  // 입력받은 문자열을 숫자로 변환
      
      //또는 int num = scanner.nextInt(); 로 받을수도 있다. 

        System.out.println("입력내용 : " + input);
        System.out.printf("num=%d%n", num);
    }
}
```
입력받은 문자열이 숫자외의 값을 포함하고 있다면 `Integer.parseInt()`에러가 발생한다.
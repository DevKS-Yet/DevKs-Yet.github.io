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

###### char타입의 표현형식
처음부터 흥미 느끼기에는 귀찮은 파트라 느껴 따로 적지는 않는다. 그래도 한번 가볍게 흝어보자. 적어도 뭔가 들으면 기억은 나야하지 않겠는가?

###### 인코딩과 디코딩(encoding & decoding)
이 부분은 char타입의 표현형식에 대해서 공부하다보면 자연스럽게 올 것이다. 참고로 encode는 '~을 코드/암호화하다'라는 것이고 decode는 그 반대다.

###### 코드 형식
이후에는 코드 형식인 ASCII, Extended ASCII, code page, Unicode, UTF-8, UTF-16 등에 대해서 나오지만 가볍게 패스한다. 대학교 시험보는 것도 아니고 간략하게만 흝고 지나가길 바란다.


### 4.3 정수형 - byte, short, int, long
여기서는 간략하게 타입과 저장 가능한 값의 범위과 크기는 꼭 알아두자. 1자리수까지 외우라는게 아니라 대략이라는 숫자라는 알고 넘어가자

| 타입 | 저장 가능한 값의 범위 | 크기(byte) |
|:---:|:---:|:---:|
| byte | -128 ~ 127 | 1 |
| short | -3,2768 ~ 3,2767 | 2 |
| int | -21,4748,3648 ~ 21,4748,3647 | 4 |
| long | -922,3372,0368,5477,5808 ~ 922,3372,0368,5477,5807 | 8 |

참고로 4자릿수마다 `,`를 찍은 것은 오타가 아니다. 다만 한국 단위로 읽을려면 4자릿수마다 찍는 것이 맞아서 그렇게 찍었다.

###### 정수형의 선택기준
짧게 말하면 정수형 변수를 선언할 때는 int타입으로 하고, int의 범위(약 ±20억)를 넘는 수를 다룰 때는 long을 사용한다. 그리고 저장공간 절약이 중요할 때 byte나 short를 사용한다.

###### 정수형의 오버플로우
'오버플로우'라는 말을 문명 유저라면 한번 쯤은 들어봤겠지만 처음 듣는 사람들을 위해 설명을 하겠다.  
만약 byte의 최대값인 127에서 1을 더하면 어떻게 될까? 에러가 발생할거같다고 생각할 수 있다. 하지만 그렇지 않다. 최대값에서 1을 더하면 -128이라는 최소값이 나온다. 기억을 못하면 구글가서 `게임 문명 간디 오버플로우`를 쳐보자. 게임 개발자는 오버플로우가 아니라 의도한 것이라고 했지만.... 모르겠다.

##### 예제 2-9/ch2/OverflowEx.java
```java
class OverflowEx {
    public static void main(String[] args) {
        short sMin = -32768;
        short sMax = 32767;
        char cMin = 0;
        char cMax = 65535;

        System.out.println("sMin\t= " + sMin);
        System.out.println("sMin-1\t= " + (short)(sMin-1));
        System.out.println("sMax\t= " + sMax);
        System.out.println("sMax+1\t= " + (short)(sMax+1));
        System.out.println("cMin\t= " + cMin);
        System.out.println("cMin-1\t= " + (int)(--cMin));
        System.out.println("cMax\t= " + cMax);
        System.out.println("cMax+1\t= " + (int)(++cMax));
    }
}
```

> 4일차는 여기까지 적어두겠다.  
> 오버플로우 은근히 재미있으니 여러가지 실험을 해보길 바란다. 5일차에는 Chapter 2를 끝내도록 하겠다.
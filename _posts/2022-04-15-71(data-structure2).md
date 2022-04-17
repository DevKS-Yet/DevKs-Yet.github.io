---
title: "배열"
excerpt: "Array"

categories:
- Data-Structure

tags:
- data structure
- data
- structure
- static
- array
---

# 자료 구조 목차

- Data-Structure
  - Linear
    - Static
      - Array
    - Dynamic
      - Linked List
      - Stack
      - Queue
  - Non Linear
    - Tree
    - Graph

지난번 포스팅에서 자료 구조의 전체적인 것에 대해서 간략하게 살펴보았다. 이제부터는 최하위 레벨에 있는 자료 구조에 대해서 하나씩 알아보자

### 배열(Array)
자바에서의 배열은 같은 타입의 변수들을 공통된 이름으로 묶어서 저장하는 것을 뜻한다.  
C/C++에서의 배열은 자바와 다르게 작동한다.

###### 자바 배열의 특징
- 자바의 모든 배열의 주소가 동적으로 할당된다.
- 자바의 Array는 객체임으로 객체의 메소드인 `length`를 사용해서 배열의 길이를 알아낼 수 있다. C/C++은 `sizeof`를 사용
- 자바의 배열 선언은 다른 변수 선언과 동일하며 데이터 타입 이후에 `[]`를 붙여준다.
- 배열 안의 변수들은 순서대로 들어가있으며 각각 인덱스가 부여된다. 해당 인덱스는 0부터 시작한다.
- 자바 배열은 정적 필드(static field), 지역 변수(local variable) 또는 메서드 매개변수(method parameter)로도 사용할 수 있다.
- 배열의 사이즈는 `int`형과 동일 또는 작은 값을 갖고 있는 정수 타입(char, byte, short)으로 선언할 수 있으며 `long` 타입으로는 할 수 없다(`length`의 리턴값이 `int`형이기에 2^31보다 작은 값을 허용하는 타입만 넣을 수 있다).
- 배열 타입의 슈퍼클래스는 Object이다(IntelliJ 사용시 `java.lang.reflect`안에 있는 `Array`을 열은 후에 `ctrl + alt + h`를 누르면 관계를 볼 수 있다).
- 모든 배열 타입은 `Cloneable`과 `java.io.Serializable`의 인터페이스를 상속받는다(정확히는 implement).

배열은 기본형(`char`, `int`, etc.) 또는 객체 참조형을 담을 수 있으며 선언 시에 정의를 같이하면 된다.  
기본형 데이터 타입의 실제 값은 contiguous memory locations에 저장된다. 참조형 데이터 타입의 실제 객체는 heap segment에 저장이 된다.

#### 배열 선언 방법
```java
int intArray[];
String[] stringArray;
MyArray[] myArray;
```
위와 같이 `타입 변수명[]` 또는 `타입[] 변수명`으로 선언할 수 있다.

#### 배열 객체 생성
```java
int intArray[];
intArray = new int[5];

short arrLength = 5;  // char, byte, short, int타입만 가능
String[] stringArray = new String[arrLength];

short[] shortArray = (short[]) Array.newInstance(short.class, 4);  // 이 방법은 추천 안함. 그냥 있길래 써봄
```
배열 선언 이후 초기화를 할 수도 있고 선언과 동시에 객체 생성을 할 수도 있다.  
위와 같이 다양하게 생성할 수 있지만 `타입[] 변수명 = new 타입[길이]`를 사용하는 것을 추천한다.

#### 배열 객체 생성과 동시에 배열에 리터럴 값 넣기
```java
int[] intArray = new int[]{1, 2, 3, 4, 5};
String[] stringArray = {"This", "is", "a", "word"};  // 주로 이걸 쓴다.
```
배열 객체 생성과 동시에 리터럴 값을 선언할 시에는 길이를 따로 넣어줄 필요가 없다. 넣은 리터럴 갯수가 해당 배열의 길이가 된다.  
&#42;혹여나 엄청나게 옛날 자바 버전을 사용한다면 2번째 방법이 안될 수도 있다.

#### 배열 객체 생성 이후 리터럴 값 넣기
```java
int[] intArray = new int[5];
intArray[0] = 10;
intArray[3] = 20;  // 인덱스 순서대로 리터럴을 넣을 필요는 없지만 이렇게 띄우고 넣을 시 문제가 발생가능하기도 하고 대부분은 for문을 통해서 리터럴을 대입한다.
// intarray[5] = 50;  // 에러. 배열의 인덱스는 0부터 시작함으로 길이가 5일 경우 인덱스는 0~4까지만 사용 가능.
```
위에 언급했던 것과 같이 항상 배열의 길이와 인덱스에 대해 신경쓰자. 그리고 대부분의 배열은 순차적으로 집어넣는 데이터들이 많기에 반복문과 같이 사용하는 경우가 많다.

#### 다차원 배열
지금까지는 1차원적인 배열만 생성했지만 배열안에 배열을 또 넣을 수가 있다. 선언 방식은 1차원과 비슷함으로 배열 선언, 배열 생성 그리고 리터럴값 대입까지 한번에 적겠다.

```java
int[][] intTwoDimensionArray;
intTwoDimensionArray = new int[3][3];  // 3개의 길이를 갖고 있는 배열 3개를 생성.

int[][][] intThreeDimensionArray = { { {1, 2, 3}, {4, 5, 6} }, { {7, 8, 9}, {10, 11, 12} }, { {13, 14, 15} } };  // 생성과 동시에 리터럴값 대입
```
딥러닝이나 알고리즘을 깊게 공부하시는 분이 아닌이상 2차원 배열, 최대는 3차원 배열정도까지만 사용할 것이다. 대부분은 1차 배열로 해결될 것이다.  
&#42; 만들 일은 없겠지만 최대 255차원까지 만들 수 있다.

#### 1차원 배열 생성부터 출력
```java
public class ArraySample1 {
    public static void main(String[] args) {
        System.out.println("-----intOneDimensionArray Start-----");
        String[] stringOneDimensionArray = {"1", "2", "3"};  // 객체 생성 및 값 대입
        for (int i=0; i<stringOneDimensionArray.length; i++) {
            System.out.print(stringOneDimensionArray[i] + "\t");
        }
        System.out.println();
        System.out.println("-----intOneDimensionArray Finish-----\n");
  
        System.out.println("-----intTwoDimensionArray Insert Start-----");
        String[][] stringTwoDimensionArray = new String[3][3];
        for (int i=0; i<stringTwoDimensionArray.length; i++) {
            for (int j=0; j< stringTwoDimensionArray[i].length; j++) {
                stringTwoDimensionArray[i][j] = ""+i+j;
            }
        }
        System.out.println("-----intTwoDimensionArray Insert End-----\n");
  
        System.out.println("-----intTwoDimensionArray Print Start-----");
        for (int i=0; i< stringTwoDimensionArray.length; i++) {
            for (int j=0; j<stringTwoDimensionArray[i].length; j++) {
                System.out.print(stringTwoDimensionArray[i][j] + "\t");
            }
            System.out.println();
        }
        System.out.println("-----intTwoDimensionArray Print End-----\n");
  
        System.out.println("-----intThreeDimensionArray Insert Start-----");
        String[][][] stringThreeDimensionArray = new String[5][4][3];
        for (int x=0; x<stringThreeDimensionArray.length; x++) {
            for (int y=0; y<stringThreeDimensionArray[x].length; y++) {
                for (int z=0; z<stringThreeDimensionArray[x][y].length; z++) {
                    stringThreeDimensionArray[x][y][z] = ""+x+y+z;
                }
            }
        }
        System.out.println("-----intThreeDimensionArray Insert End-----\n");
  
        System.out.println("-----intThreeDimensionArray Print Start-----");
        for (int x=0; x<stringThreeDimensionArray.length; x++) {
            for (int y=0; y<stringThreeDimensionArray[x].length; y++) {
                for (int z=0; z<stringThreeDimensionArray[x][y].length; z++) {
                    System.out.print(stringThreeDimensionArray[x][y][z] + "\t");
                }
                System.out.println();
            }
            System.out.println();
        }
        System.out.println("-----intThreeDimensionArray Print End-----");
    }  //main
}
```

#### 배열을 위한 Object 메서드(class Objects for Arrays)
```java
public class ArraySample2 {
    public static void main(String[] args) {
        int intArray[] = new int[3];
        byte byteArray[] = new byte[3];
        short shortArray[] = new short[3];
        String[] strArray = new String[3];

        System.out.println("intArray.getClass() = " + intArray.getClass());
        System.out.println("byteArray.getClass() = " + byteArray.getClass());
        System.out.println("shortArray.getClass() = " + shortArray.getClass());
        System.out.println("strArray.getClass() = " + strArray.getClass());
        System.out.println("strArray.getClass().getSuperclass() = " + strArray.getClass().getSuperclass());
```

#### 배열 복사(Cloning of arrays)
```java
public class ArraySample3 {
    public static void main(String[] args) {
        int originalArray[] = {1, 2, 3};
        int cloneArray[] = originalArray.clone();
        System.out.println("originalArray == cloneArray : " + (originalArray==cloneArray));
        for (int i=0; i<cloneArray.length; i++) {
            System.out.print(cloneArray[i] + "\t");
        }
        System.out.println();
    }
}
```
복사를 했다면 같은 참조변수를 볼줄 알았지만 아니다. 새로운 객체를 생성하게 된다.  
하지만 다차원일 경우에는 조금 다르다.

####
```java
public class ArraySample4 {
    public static void main(String[] args) {
        int originalArray[][] = {{1, 2, 3}, {4, 5, 6}};
        int cloneArray[][] = originalArray.clone();
        System.out.println("originalArray == cloneArray : " + (originalArray == cloneArray));
        System.out.println("originalArray[0] == cloneArray[0] : " + (originalArray[0] == cloneArray[0]));
        System.out.println("originalArray[1] == cloneArray[1] : " + (originalArray[1] == cloneArray[1]));
    }
}
```
결과가 신기하게도 `originalArray`의 참조를 따라가지는 않지만 그 하위에 있는 배열들은 같은 곳을 참조한다.

> 적다보니 많이 길어졌다. 이렇게까지 적을 생각은 없었지만...  
> 물론 이런 속성을 다 외울 필요는 없다고 생각한다. 다만 배열과 for문 또는 while문으로 무언가를 만들어보길 바란다. 익숙해지면 할 수 있는 것도 많아지고 재미도 있다.

### Reference
- [https://www.geeksforgeeks.org/introduction-to-arrays/?ref=lbp](https://www.geeksforgeeks.org/introduction-to-arrays/?ref=lbp)
- [https://www.geeksforgeeks.org/arrays-in-java](https://www.geeksforgeeks.org/arrays-in-java/)
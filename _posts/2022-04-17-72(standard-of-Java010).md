---
title: "자바의 정석 10일차"
excerpt: "post"

categories:
- standard-of-java
tags:
- java
- book
---

# Chapter 04 조건문과 반복문(if, switch, for, while statement)

## 2.반복문 - for, while, do-while

### 2.2 while문
for문에 비해 while문은 구조가 간단하다. 조건식만 있으면 while문 괄호{} 내의 문장을 반복한다.

```java
while (조건식) {
    // 조건식의 연산결과가 참(true)인 동안, 반복될 문장들을 적는다.
}
```
for문과 비교하면 초기화 및 증감식이 없다는 것을 확인할 수 있다.

###### for문과 while문의 비교
1부터 10까지의 정수를 순서대로 출력하는 for문을 while문으로 변경하면 다음과 같다.

```java
function forStatement() {
    // 초기화, 조건식, 증감식
    for (int i=1; i<=10; i++) {
        System.out.println(i);
    }
}

function whileStatement() {
    int i=1;  // 초기화
    while (i<=10) {  // 조건식
        System.out.println(i);
        i++;  // 증감식
    }
}
```
이렇게 보면 while문을 작성할때 초기화와 증감식만 안들어가지 필수적으로 들어가야하는 것처럼 보인다. for문과 while문은 항상 서로 변환 또한 가능하다.  
그렇다면 언제 while문을 쓰면 좋을지 다음 예제들을 통해서 알아보자.  
~~불편하면 그냥 for문만 써도 된다~~

###### while문의 조건식은 생략불가
한 가지 주의할 점은 for문과 달리 while문의 조건식은 생략할 수 없다는 것이다.

```java
while () {  // 에러. 조건식이 없음.
    ....
}
```

##### 예제 4-23/ch4/FlowEx23.java
```java
class FlowEx23 {
    public static void main(String[] args) {
        int i = 5;  // 초기화
        
        while (i-- != 0) {  // 조건식과 증감식
            System.out.println(i + " - What\'s \'i-- != 0\'");
        }
    }
}
```
위 예제에서 'i--' 대신 '--i'를 사용한다면 어떤 결과를 얻을지 예측해보고 실제로 실행도 해보자.

##### 예제 4-24/ch4/FlowEx24.java
```java
class FlowEx24 {
    public static void main(String[] args) {
        int i=11;
        System.out.println("카운트 다운을 시작합니다.");
        
        while (i-- != 0) {
            System.out.println(i);
            for (int j=0; j<2_000_000_000; j++);
        }
        System.out.println("GAME OVER")
    }
}
```
for문은 시간을 조금씩 지연시켜서 출력시키기 위함이니 반복횟수는 적절히 변경하거나 `Thread.sleep()`을 사용할 수도 있다.

##### 예제 4-25/ch4/FlowEx25.java
```java
import java.util.*;

class FlowEx25 {
    public static void main(String[] args) {
        int num = 0, sum = 0;
        System.out.println("숫자를 입력하세요. (예:12345)>");
        
        Scanner scanner = new Scanner(System.in);
        String tmp = scanner.nextLine();
        num = Integer.parseInt(tmp);  // 또는 num = scanner.nextInt(); 로 바로 받을수도 있다.
        
        while (num != 0) {
            sum += num%10;  // sum = sum + num%10
            System.out.printf("sum = %3d, num = %d%n", sum, num);
            
            num /= 10;  // num = num / 10;
        }
        System.out.println("각 자리수의 합 : " + sum);
    }
}
```
처음보면 이게 뭘 위한 것인지와 어떻게 돌아가는지 궁금할 수도 있다. 뭘 위한 것인지는 나도 어디에 쓸 수 있는지는 아직도 모른다... 하지만 어떻게 돌아가는지는 확인하자

##### 예제 4-26/ch4/FlowEx26.java
```java
class FlowEx26 {
    public static void main(String[] args) {
        int sum = 0;
        int i = 0;
        
        // i를 1씩 증가시켜서 sum에 계속 더해나간다.
        while ((sum += i++) <= 100) {
            System.out.printf("%d - %d%n", i, sum);
        }
    }
}
```
이렇게 한다면 몇번째에서 더한 숫자가 합계가 100을 초과하지 않는지 확인할 수 있다.

##### 예제 4-27/ch4/FlowEx27.java
```java
class FlowEx27 {
    public static void main(String[] args) {
        int num;
        int sum = 0;
        boolean flag = true;
        Scanner scanner = new Scanner(System.in);
        
        System.out.println("합계를 구할 숫자를 입력하세요.(끝내려면 0을 입력)");
        
        while (flag) {
            System.out.println(">>");
            
            String tmp = scanner.nextLine();
            num = Integer.parseInt(tmp);
            
            if (num != 0) {
                sum += num;
            } else {
                flag = false;
            }
        }
        System.out.println("합계 : " + sum);
    }
}
```
조건문인 if문을 통해서 while의 조건식을 제어할 수도 있다.

### 2.3 do-while문
do-while문은 while문의 변형으로 기본적인 구조는 while문과 같으나 조건식과 블럭의 순서를 바꿔놓은 것이다. 그래서 while문과는 반대로 블럭을 먼저 수행한 후에 조건식을 평가한다.  
while문과 do-while문의 차이점은 while문은 블럭이 한 번도 수행되지 않을 수 있지만, do-while문은 최소한 한번은 수행도리 것을 보장한다.

```java
do {
    // 조건식의 연산결과가 참일 때 수행될 문장들을 적는다.
} while (조건식);  // 끝에 ';'을 잊지 않도록 주의
```

##### 예제 4-28/ch4/FlowEx28.java
```java
import java.util.*;

class FlowEx28 {
    public static void main(String[] args) {
        int input = 0, answer = 0;
        
        answer = (int) (Math.random() * 100) + 1;  // 1~100사이의 임의의 수를 저장
        Scanner scanner = new Scanner(System.in);
        
        do {
            System.out.print("1과 100사이의 정수를 입력하세요.>");
            input = scanner.nextInt();
            
            if (input > answer) {
                System.out.println("더 작은 수로 다시 시도해보세요.");
            } else if (input < answer) {
                System.out.println("더 큰 수로 다시 시도해보세요.");
            }
        } while (input != answer);
        System.out.println("정답입니다.");
    }
}
```
재미있는 숫자 맞추기 게임이다. do-while말고도 while문으로도 작성은 가능하다.

##### 예제 4-29/ch4/FlowEx29.java
```java
class FlowEx29 {
    public static void main(String[] args) {
        for (int i=1; i<=100; i++) {
            System.out.printf("i=%d ", i);
            
            int tmp = i;
            
            do {
                if (tmp%10%3 == 0 && tmp%10 != 0) {
                    System.out.print("짝");
                }
            } while ((tmp/=10) != 0);
            System.out.println();
        }
    }
}
```
재미있는 369게임이다. 하지만 여기서는 3의 배수인 12나 15같은 것들은 제외되어있다. 3의 배수들도 체크될 수 있도록 해보자.

### 2.4 break문
조건식인 switch문에서 break를 사용한 적이 이싿. 반복문에서도 break문을 사용할 수 있는데, switch문에서 그랬던 것처럼, break문은 자신이 포함된 가장 가까운 반복문을 벗어난다. 주로 if문과 함께 사용되어 특정 조건을 만족하면 반복문을 벗어나도록 한다.

##### 예제 4-30/ch4/FlowEx30.java
```java
class FlowEx30 {
    public static void main(String[] args) {
        int sum = 0;
        int i = 0;
        
        while (true) {
            if (sum > 100) break;
            ++i;
            sum += i;
        }
        System.out.println("i = " + i);
        System.out.println("sum = " + sum);
    }
}
```
예제 4-26과 같다.


### 2.5 continue문
continue문은 반복문 내에서만 사용될 수 있으며, 반복이 진행되는 도중에 continue문을 만나면 반복문의 끝으로 이동하여 다음 반복으로 넘어간다.  
for문의 경우 증감식으로 이동하며, while문과 do-while문의 경우 조건식으로 이동한다.

##### 예제 4-31/ch4/FlowEx31.java
```java
class FlowEx31 {
    public static void main(String[] args) {
        for (int i=0; i<=10; i++) {
            if (i%3 == 0) {
                continue;
            }
            System.out.println(i);
        }
    }
}
```
보면 `i%3 == 0`을 만족하는 숫자는 다음 반복문으로 넘어간 것을 확인할 수 있다.

##### 예제 4-32/ch4/FlowEx32.java
```java
import java.util.*;

class FlowEx32 {
    public static void main(String[] args) {
        int menu = 0;
        int num = 0;
        
        Scanner scanner = new Scanner(System.in);
        
        while (true) {
            System.out.println("(1) square");
            System.out.println("(2) square root");
            System.out.println("(3) log");
            System.out.print("원하는 메뉴 (1~3)를 선택하세요. (종료:0)>");
            
            String tmp = scanner.nextLine();
            menu = Integer.parseInt(tmp);
            
            if (menu == 0) {
                System.out.println("프로그램을 종료합니다.");
                break;
            } else if (!(1 <= menu && menu <= 3)) {
                System.out.println("메뉴를 잘못 선택하셨습니다.(종료는 0)");
                continue;
            }
            System.out.println("선택하신 메뉴는 " + menu + "번입니다.");
        }
    }
}
```
뭔가 살짝 아쉬운 예제이다. Math 클래스에서 pow, sqrt 그리고 log가 있으니 해당 메서드를 참고해서 자기 입맛대로 좀 더 추가해보자.  
참고로 못해도 괜찮다. 곧 발전시킨 예제가 나올 것이다.


### 2.6 이름 붙은 반복문
break문은 근접한 단 하나의 반복문만 벗어날 수 있기 때문에, 여러 개의 반복문이 중첩된 경우에는 break문으로 중첩 반복문을 완전히 벗어날 수 없다.  
이때는 중첩 반복문 앞에 이름을 붙이고 break문과 continue문에 이름을 지정해 줌으로써 하나 이상의 반복문을 벗어나거나 반복을 건너뛸 수 있다.

##### 예제 4-33/ch4/FlowEx33.java
```java
class FlowEx33 {
    public static void main(String[] args) {
        Loop1 :
        for (int i=2; i<=9; i++) {
            for (int j=1; j<=9; j++) {
                if (j == 5) {
                    break Loop1;
//                    break;
//                    continue Loop1;
//                    continue;
                }
                System.out.println(i + "*" + j + " = " + i*j);
            }  // continue;
            System.out.println();  // break;
        }  // continue Loop1;
        // break Loop1;
    }
}
```
위와 같이 사용할 수 있다. 각 break문과 continue문이 어딜로 가는지 확인해두면 좋을 듯하다.

##### 예제 4-34/ch4/FlowEx34.java
```java
import java.util.*;

class FlowEx34 {
    public static void main(String[] args) {
        int menu = 0, num = 0;
        
        Scanner scanner = new Scanner(System.in);
        
        outer:
        while (true) {
            System.out.println("(1) square");
            System.out.println("(2) square root");
            System.out.println("(3) log");
            System.out.print("원하는 메뉴 (1~3)를 선택하세요. (종료:0)>");
            
            String tmp = scanner.nextLine();
            menu = Integer.parseInt(tmp);
            
            if (menu == 0) {
                System.out.println("프로그램을 종료합니다.");
                break;
            } else if (!(1 <= menu && menu <= 3)) {
                System.out.println("메뉴를 잘못 선택하셨습니다.(종료는 0)");
                continue;
            }
            for (;;) {  // while(true)와 동일한 뜻이다.
                System.out.print("계산할 값을 입력하세요. (계산 종료:0, 전체 종료:99");
                tmp = scanner.nextLine();
                num = Integer.parseInt(tmp);
                
                if (num == 0) break;
                if (num == 99) break outer;
                switch (menu) {
                  case 1:
                      System.out.println("result = " + num*num);
                      break;
                  case 2:
                      System.out.println("result = " + Math.sqrt(num));
                      break;
                  case 3:
                      System.out.println("result = " + Math.log(num));
                      break;
                }  // switch
            }  // for(;;)
        }  // while
    }  // main
}
```
예제 4-32에서 아쉬웠던 점들이 추가된 예제이다. 뭔가 더 생각나는 것들이 있다면 case에 추가하여 더 추가해보자.

> 이것으로 Chapter04 조건문과 반복문이 끝났다. 프로그래밍에서 정말정말 중요한 부분이니 이해가 안된 부분 있다면 꼭 다시 읽고 예제를 그냥 따라 적는 것이 아니라 자신의 입맛에 따라서 변경도 해보자  
> Chatper05 배열은 지금 조금 고민중에 있다. 주소값 같은 것을 언급하면 블로그 차단을 하지않을까 하는 생각이다...... 일단 적어보고 의견을 받아서 수정을 계속하도록 해보겠다.
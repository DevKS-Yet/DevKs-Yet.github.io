---
title: "13&#46; Break and Continue"
excerpt: "기본 자바"

categories:
  - 자바(기본)
tags:
  - 자바
  - java
  - basic
  - break
  - continue
---

## 브레이크(Break)
- 저번에 스위치문에 대해서 포스팅할때에 break라는 것을 사용해서 탈출이라는 용도로 사용하였습니다.
- 해당 break문은 스위치문 뿐만 아니라 while문과 for문에서도 같은 용도로 사용을 할 수 있습니다.
- i가 4와 같을 때 for문을 멈추도록 하는 예시입니다.
```java
int (int i=0; i<10; i++) {
  if (i == 4) {
    break;
  }
  System.out.println(i);
}
```

## 컨티뉴(Continue)
- Continue는 탈출이 아니라 한번 스킵 개념으로 생각하시면 쉽겠습니다.
- 4를 스킵하는 예시입니다.
```java
for (int i=0; i<10; i++) {
  if (i == 4) {
    continue;
  }
  System.out.println(i);
}
```

## while문에서 사용 예시
- Break 예시
```java
int i = 0;
while (i < 10) {
  System.out.println(i);
  i++;
  if (i == 4) {
    break;
  }
}
```
- Continue 예시
```java
int i = 0;
while (i < 10) {
  if (i == 4) {
    i++;
    continue;
  }
  System.out.println(i);
  i++;
}
```

# 🧠 자바 참조 타입과 참조 변수 _ Chap 05-1

> 🏷️ Tags: `Java`, `참조타입`, `기본타입`, `String`, `null`, `Week5`

---

## ✨ 학습 키워드

- 기본 타입 vs 참조 타입 차이 이해하기
- 참조 타입 변수에 null 할당 가능성 이해하기
- NullPointerException 발생 원리 파악
- String 객체의 특징과 비교 연산 결과 분석

---

## 📌 기본 타입과 참조 타입

| 항목          | 기본 타입                        | 참조 타입                            |
|---------------|----------------------------------|----------------------------------------|
| 저장 내용     | 실제 값 (리터럴)                | 메모리 주소 (객체의 위치)             |
| 예시 타입     | int, double, boolean 등          | 배열, String, 클래스, 인터페이스 등     |
| 초기값        | 숫자는 0, boolean은 false 등     | null (주소 없음)                      |

---

## 🧠 메모리 사용 영역 개요

- 🏛️ 메소드 영역: 클래스, static 변수, 메소드 정보 저장
- 🧊 힙(Heap) 영역: new로 생성된 객체, 배열이 저장됨
- 🧮 JVM 스택 영역: 메소드 호출 시마다 프레임 생성

📌 스택 영역 특징:

- 기본 타입 변수 → 스택에 값 자체 저장  
- 참조 타입 변수 → 힙의 주소값 저장  
- 블록이 끝나면 자동으로 스택에서 제거됨

---

## 📌 null 값 이란?
🔎 특징:
- 참조 타입 변수는 null을 가질 수 있음
- null인지 여부는 비교 연산자(==, !=)로 확인 가능
- null 상태에서 객체의 필드나 메소드를 호출하면 예외 발생
  → NullPointerException

### 💻 예제 

```java
String str1 = null;
String str2 = "hello";

System.out.println(str1 == null);     // true
System.out.println(str2 != null);     // true
System.out.println(str1 == str2);     // false
```


---

## 📌 문자열 (String) 타입이란?

- 문자열을 저장하고 처리하는 데 사용되며, 기본 타입처럼 다뤄질 수 있지만 사실은 객체임
- 문자열 선언 시, 쌍따옴표를 사용해야함


### ✨ 문자열 선언 방법

| 선언 방식                           | 설명                                                       |
|------------------------------------|------------------------------------------------------------|
| String str = "hello";              | 문자열 리터럴. 상수풀(String Pool)에 저장됨               |
| String str = new String("hello");  | new 연산자로 객체 생성. 힙 메모리에 새로운 객체 생성됨    |


### ✨ 문자열 비교 방식

| 비교 방식       | 의미                          | 사용 메소드/연산자     |
|----------------|-------------------------------|------------------------|
| 주소(참조) 비교 | 두 변수의 객체 주소가 같은가? | == 또는 !=             |
| 내용 비교       | 문자열 안의 글자가 같은가?     | equals() 메소드        |

#### ⚠️ 주의할 점
- == 연산자는 “같은 객체(주소)인가?”만 비교 가능함
- 문자열 값이 같아도 new String()으로 만든 객체는 주소가 다르기 때문에 ==은 false가 나옴
- 문자열 내용 비교는 반드시 equals() 메소드를 사용

### 💬 문자열 예시

```java
String a = "hello";
String b = "hello";
String c = new String("hello");

System.out.println(a == b);         // true - 같은 리터럴 → 같은 주소
System.out.println(a == c);         // false - new로 생성된 별도 객체
System.out.println(a.equals(c));    // true - 문자열 내용은 같음

```

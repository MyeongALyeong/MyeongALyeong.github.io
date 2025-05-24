# Chap 10. 예외 처리

## 10-1️⃣ 예외 클래스

### ⚠️ 예외와 예외 클래스

* 예외 정의: 사용자의 잘못된 조작 또는 개발자의 코딩 실수로 발생하는 프로그램 오류임.
* 예외 역할: 예외 처리로 프로그램 종료 없이 정상 실행 유지함.
* 예외 관리: 자바에서 예외를 클래스로 관리함. 모든 예외 클래스는 `java.lang.Exception` 상속함.

### 🛠️ 예외 종류

| 구분                          | 설명                                                             |
| --------------------------- | -------------------------------------------------------------- |
| 일반 예외 (Checked Exception)   | 컴파일 시점에 예외 처리 코드 유무 검사함. 미작성 시 컴파일 오류 발생함.                     |
| 실행 예외 (Unchecked Exception) | `RuntimeException` 하위 클래스. 실행 중 예측 불가능한 오류 발생함. 컴파일러가 체크하지 않음. |

#### 🏷️ 대표 실행 예외

* `NullPointerException`: null 참조 변수로 메서드 호출 또는 필드 접근 시 발생함.
* `ArrayIndexOutOfBoundsException`: 배열 인덱스 범위 초과 접근 시 발생함.
* `NumberFormatException`: 숫자 변환 메서드에 숫자로 변환 불가능한 문자열 전달 시 발생함.

##### NumberFormatException 메서드

| 리턴 타입    | 메서드 이름                         | 설명                     |
| -------- | ------------------------------ | ---------------------- |
| `int`    | `Integer.parseInt(String s)`   | 주어진 문자열을 정수로 변환하여 리턴함. |
| `double` | `Double.parseDouble(String s)` | 주어진 문자열을 실수로 변환하여 리턴함. |

* `ClassCastException`: 상속 관계가 없는 클래스 간 타입 캐스팅 시 발생함.

## 10-2️⃣ 예외 처리

### 🎯 예외 처리 코드 (try-catch-finally)

* `try` 블록: 예외 발생 가능 코드 작성함.
* `catch` 블록: 발생한 예외 타입별 처리 코드 작성함.
* `finally` 블록: 예외 발생 여부 관계없이 항상 실행할 코드 작성함.

```java
try {
    // 예외 발생 가능 코드
    String text = null;
    System.out.println(text.length()); // NullPointerException 발생
} catch (NullPointerException e) {
    System.err.println("null 참조 접근 시도함: " + e.getMessage());
} finally {
    System.out.println("예외 처리 완료함.");
}
```

### 📝 예외 종류에 따른 처리 (다중 catch)

* `try` 블록에서 여러 타입 예외 발생 가능함.
* `catch` 블록은 위에서부터 매칭되며 하나의 `catch`만 실행됨.
* 상위 예외 클래스는 하위 예외 클래스 아래에 위치시켜야 함.

```java
try {
    int[] arr = new int[3];
    System.out.println(arr[5]); // ArrayIndexOutOfBoundsException 발생
    Integer.parseInt("ABC");   // NumberFormatException 발생
} catch (ArrayIndexOutOfBoundsException | NumberFormatException e) {
    System.err.println("배열 또는 형식 오류 발생함: " + e.getClass().getSimpleName());
} catch (Exception e) {
    System.err.println("기타 예외 처리함: " + e);
}
```

### ↩️ 예외 떠넘기기 (throws)

* `throws` 키워드: 메서드 선언부에 사용하여 예외를 호출한 곳으로 전달함.
* throws 대상: Checked Exception만 선언 가능함.

```java
public void readFile(String path) throws IOException {
    FileInputStream fis = new FileInputStream(path);
    // 파일 읽기 코드
}
```

* 호출부에서 `try-catch`로 처리함.

```java
try {
    readFile("data.txt");
} catch (IOException e) {
    System.err.println("파일 읽기 실패함: " + e.getMessage());
}
```

💡 **Tip**: `RuntimeException` 계열 예외는 `throws` 선언 없이 호출부에서 처리하거나 넘길 수 있음.

---

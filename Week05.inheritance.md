# 🧠 Java - 상속, 다형성, 추사 클래스 정보

## 📘 07-1. 클래스 상속

### ✅ 기본 객념

- 클래스 상속은 기존 클래스(부모 클래스)의 필드가 또는 메소드를 **자식 클래스**에서 사용할 수 있도록 해주는 것
- `extends` 키워드 사용

```java
class Parent {
    void hello() {
        System.out.println("Hello from Parent");
    }
}

class Child extends Parent {
    void hi() {
        System.out.println("Hi from Child");
    }
}
```

### 🔒 접근 제한자에 따른 상속 가능 여부

| 접근 제한자 | 같은 패키지 | 다른 패키지 |
|----------------|----------------|----------------|
| `public`       | ✅ 가능     | ✅ 가능     |
| `protected`    | ✅ 가능     | ✅ 가능     |
| (default)      | ✅ 가능     | ❌ 불가능  |
| `private`      | ❌ 불가능  | ❌ 불가능  |

---

### 👨‍👩‍👧 부모 생성자 호출

- 자식 객체를 생성하면 **부모 객체 먼저 호출**
- 자식 생성자에서 부모 생성자를 명시화: `super(...)`

```java
class Parent {
    Parent(String msg) {
        System.out.println("Parent 생성자: " + msg);
    }
}

class Child extends Parent {
    Child() {
        super("부모에게 전달할 메시지");
        System.out.println("Child 생성자");
    }
}
```

#### 부모에 기본 생성자가 없고 메가번수 생성자만 있는 경우:

```java
class Parent {
    Parent(String name) {
        System.out.println("Hello " + name);
    }
}

class Child extends Parent {
    Child(String name) {
        super(name); // 마지막에서가 아니라 첫 줄에 위치
    }
}
```

#### `super()` vs `super.`

| 구단        | 설명                          |
|-------------|---------------------------------|
| `super()`   | 부모 클래스의 생성자 호출   |
| `super.`    | 부모 클래스의 메소드/필드 호출 |

---

### ✏️ 메소드 오버라이드 & `super` 사용

```java
class Parent {
    void greet() {
        System.out.println("Hello from Parent");
    }
}

class Child extends Parent {
    @Override
    void greet() {
        super.greet();
        System.out.println("Hello from Child");
    }
}
```

---

## 🧬 07-2. 타입 변환과 다형성

### 🔄 자동 타입 변환 (Upcasting)

```java
Parent p = new Child();
p.greet();  // 자식의 오버라이드 메소드 호출
```

### 🧪 필드와 메가리바수의 다형성

```java
class Animal {
    void sound() {
        System.out.println("동물 소리");
    }
}

class Dog extends Animal {
    @Override
    void sound() {
        System.out.println("몬몬");
    }
}

class Zoo {
    void makeSound(Animal a) {
        a.sound();
    }
}
```

---

### 🔁 강제 타입 변환 (Downcasting)

```java
Animal a = new Dog();

if (a instanceof Dog) {
    Dog d = (Dog) a;
    d.sound();
}
```

---

## 🧱 07-3. 추사 클래스

### 📌 추사 클래스의 용단

- 공통 기본 형태와 기능 설정
- 객체 생성 특정: ❌

### ✍️ 선언 예시

```java
abstract class Animal {
    abstract void sound();
}

class Cat extends Animal {
    @Override
    void sound() {
        System.out.println("야옴");
    }
}
```

```java
Animal a = new Cat(); // O
Animal b = new Animal(); // X
```

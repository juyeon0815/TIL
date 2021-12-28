# static

---

### 1️⃣ static

- 고정된이란 의미

- 메모리에 한번 할당되어 프로그램이 종료될 때 해제되는 것

  

[Static 메모리]

![STUN](/res/static.png)

- Class는 Static영역에 생성, new 연산을 통해 생성한 객체는 Heap영역에 생성

- static 키워드를 통해 static 영역에 할당된 메모리는 모든 객체가 공유하는 메모리
  
    ⇒ GC가 관리하지 않기 때문에 Static을 자주 사용하면 프로그램의 종료시까지 메모리가 할당된 채로 존재하므로 악영향을 줄 수 있음
    
    

### 2️⃣ static 특징

- 객체를 생성하지 않고도 static 자원에 접근이 가능하다.

- 전역 변수와 비슷한 특징을 가지며 공간을 할당받고 초기화가 이루어지면 프로그램이 종료될 때까지 소멸이 일어나지 않는다.

  

### 3️⃣ static 변수

- 메모리에 한번 할달되어 프로그램이 종료될 때 해제되는 변수
- 여러 객체가 해당 메모리를 공유

```java
public class Person {
	String name = "JuYeon";

	public static void main(String[] args){
		Person per = new Person();
		Person per2 = new Person();
	}
}
```

- 위와 같이 클래스를 만들고 객체를 생성하면 객체마다 객체변수 name을 저장하기 위한 메모리가 별도로 할당

- 어떤 객체이던지 동일한 값일 경우 static 사용 시 메모리의 이점을 얻을 수 있다.

  

```java
public class Person {
	static String name = "JuYeon";

	public static void main(String[] args){
		Person per = new Person();
		Person per2 = new Person();
	}
}
```

- name 변수에 static 키워드를 붙이면 메모리 할당을 딱 한번 하기 때문에 메모리 사용에 이점이 있다.

- 만약, name 변수가 변경되지 않기를 바란다면 static 키워드 앞에 `final` 이라는 키워드 붙이기

  

### 4️⃣ static 메소드

- 객체 생성 없이 호출 가능 (지양)

```java
public class Counter {
	static int count = 0;
	Counter() {
		this.count++;
	}

	public static int getCount() {
		return count;
	}
	
	public static void main(Stirng[] args) {
		Counter c1 = new Counter();
		Counter c2 = new Counter();
	
		System.out.println(Counter.getCount()); //객체 생성없이 직접 호출O
	}
}
```

- static 메소드는 유틸리성 메소드를 작성할 때 많이 사용
    - ex) Date , Math 등
# ListIterator

---

### 1️⃣ Iterator<E> 인터페이스

- 컬렉션에 저장된 요소를 읽어오는 방법을 iterator인터페이스로 표준화

```java
LinkedList<Integer> list = new LinkedList<Integer>();

list.add(4);
list.add(3);
list.add(2);
list.add(1);

Iterator<Integer> iter = list.iterator();

while(iter.hasNext()){ //hasNext : 다음 요소를 가지고 있으면 true / 아니면 false 반환
	System.out.print(iter.next()+" "); //next : 다음 요소 반환
}

// 4 3 2 1
```

### 2️⃣ ListIterator<E> 인터페이스

- Iterator 인터페이스를 상속받아 여러 기능을 추가한 인터페이스
- Iterator 인터페이스는 컬렉션 요소에 접근할 때 한 방향으로만 이동할 수 있지만 ListIterator 인터페이스는 양방향으로 이동할 수 있다.

```java
LinkedList<Integer> list = new LinkedList<Integer>();

list.add(4);
list.add(2);
list.add(3);
list.add(1);

ListIterator<Integer> iter = list.listIterator();

while (iter.hasNext()) { //hasNext : 순방향으로 순회할 때 다음 요소가 있으면 true 아니면 false
    System.out.print(iter.next() + " "); //next : 다음 요소를 반환하고 커서 위치 순방향으로 이동
}

while (iter.hasPrevious()) { //hasPrevious : 역방향으로 순회할 때 다음 요소가 있으면 true 아니면 false
    System.out.print(iter.previous() + " "); //previous : 이전 요소를 반환하고 커서 위치 역방향으로 이동
}

// 4 2 3 1
// 1 3 2 4
```


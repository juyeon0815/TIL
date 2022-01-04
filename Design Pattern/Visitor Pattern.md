# Visitor Pattern

---

### 1️⃣ Visitor Pattern

- 방문자와 방문 공간을 분리하여, 방문 공간이 방문자를 맞이할 때, 이후에 대한 행동을 방문자에게 위임하는 패턴

- 알고리즘을 객체 구조에서 분리시키는 디자인 패턴
  
    ⇒ 구조를 수정하지 않고도 실질적으로 새로운 동작을 기존의 객체 구조에 추가할 수 있게 된다.
    
    ⇒ 개방-폐쇄 원칙을 적용하는 방법 중 하나
    
    

### 예시

- 쇼핑몰 고객을 등급별로 나누고 등급에 따라 혜택을 주기로 한다.
- 등급은 Gold, Vip가 있고 혜택은 포인트, 할인이 있다.
- 고객 등급별 혜택을 줄 수 있는 확장 가능한 해결책을 찾아보자.



```java
public interface Member { }

public class GoldMember implements Member { }

public class VipMember implements Member { }
```

- Member 인터페이스를 사용해서 등급별로 구체 클래스 생성



```java
public class GoldMember implements Member {
	public void point() { System.out.println("Point for Gold Member"); }
	public void discount() { System.out.println("Discount for Gold Member"); }
}

public class VipMember implements Member {
	public void point() { System.out.println("Point for Vip Member"); }
	public void discount() { System.out.println("Discount for Vip Member"); }
}
```

- 등급별 혜택 구현



```java
public class Main {
	public static void main(String[] args) {
		Member gold = new GoldMember();
		Member vip = new VipMember();

		gold.point();
		vip.point();
		gold.discount();
		vip.discount();
	}
}
//실행 결과
Point for Gold Member
Point for Vip Member
Discount for Gold Member
Discount for Vip Member
```



### ⭐ 문제점 ⭐

- 고객들에게 혜택을 주고자 할 때 명시적으로 혜택을 주기 위한 메소드를 호출해야한다.
- 혜택이 늘어났을 경우 모든 멤버들에 대해 그 혜택을 구현했다는 보장이 없다.



### ⭐ 해결방안 ⭐

![stun](/res/visitorPattern.png)



```java
public interface Benefit {
    void getBenefit(GoldMember member);
    void getBenefit(VipMember member);
}
```

- Benefit 인터페이스에 혜택을 받을 Member 별로 실행 가능한 메소드 정의



```java
public class DiscountBenefit implements Benefit {
    @Override
    public void getBenefit(GoldMember member) {
        System.out.println("Discount for Gold Member");
    }

    @Override
    public void getBenefit(VipMember member) {
        System.out.println("Discount for Vip Member");
    }
}

public class PointBenefit implements Benefit {
    @Override
    public void getBenefit(GoldMember member) {
        System.out.println("Point for Gold Member");
    }

    @Override
    public void getBenefit(VipMember member) {
        System.out.println("Point for Vip Member");
    }
}
```

- 멤버 등급별 혜택에 대해 기능 구현



```java
public interface Member {
    void getBenefit(Benefit benefit);
}
```

- 등급별 멤버가 혜택을 받을 수 있는 메소드를 Member 인터페이스에 선언



```java
public class GoldMember implements Member {
    @Override
    public void getBenefit(Benefit benefit) {
        benefit.getBenefit(this);
    }
}

public class VipMember implements Member {
    @Override
    public void getBenefit(Benefit benefit) {
        benefit.getBenefit(this);
    }
}
```

- 혜택받는 메소드 구현
- 다른 Member가 추가되더라도 구현 부분은 `benefit.getBenefit(Benefit benefit);` 만 넣으면 된다.



```java
public class Main {
    public static void main(String[] args) {
        Member goldMember = new GoldMember();
        Member vipMember = new VipMember();
        Benefit pointBenefit = new PointBenefit();
        Benefit discountBenefit = new DiscountBenefit();

        goldMember.getBenefit(pointBenefit);
        vipMember.getBenefit(pointBenefit);
        goldMember.getBenefit(discountBenefit);
        vipMember.getBenefit(discountBenefit);
    }
}

//실행 결과
Point for Gold Member
Point for Vip Member
Discount for Gold Member
Discount for Vip Member
```





### ⭐ 결과 ⭐

- Visitor 패턴에서는 혜택이 늘어나더라도 Benefit 인터페이스에 명시적으로 등급별 메소드를 정의하고 있어 구현 누락이 발생하지 않는다.
- 혜택을 추가하기 위해서 해당 혜택을 구현하는 클래스를 추가하면 되므로, 코드 중복이 발생하지 않는다.





### ⭐ Visitor 패턴을 언제 쓰면 좋을까? ⭐

- 대상 객체가 잘 바뀌지 않고, 적용할 알고리즘이 추가될 가능성이 많은 상황일 때



참고

[https://thecodinglog.github.io/design/2019/10/29/visitor-pattern.html](https://thecodinglog.github.io/design/2019/10/29/visitor-pattern.html)

[https://velog.io/@cham/Design-Pattern-방문자-패턴-Visitor-pattern](https://velog.io/@cham/Design-Pattern-%EB%B0%A9%EB%AC%B8%EC%9E%90-%ED%8C%A8%ED%84%B4-Visitor-pattern)
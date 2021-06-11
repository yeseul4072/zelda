## this

this란?

- Java에서 자신의 메모리를 가리킴(인스턴스 자신의 메모리 주소 반환)

- 생성자에서 다른 생성자를 호출 함

  

### 자신의 메모리를 가리키는 this

코드 상에서 `this`가 사용된 경우를 살펴보자.

```java
package hiding;

public class MyDate {
    private int day;
    private int month;
    private int year;
    
    public void setDay(int day) {
        this.day = day; // this = MyClass 클래스로 생성된 인스턴스 주소 반환
    }
}
```

```java
package hiding;

public class MyDateTest {
    public static void main(String[] args) {
        MyDate date = new MyDate();
        MyDate date2 = new MyDate();
        
        date.setDay(1);
        date2.setDay(2);
    }
}
```

- `date`와 `date2` 참조 변수는 각각의 인스턴스를 힙 메모리 상에 가지게 된다. 
- `setDay()` 메서드를 실행하면 **각각의 인스턴스 주소에 위치한 `day` 변수**에 입력한 값이 저장된다. 



### 생성자에서 다른 생성자를 호출하는 this

앞서 같은 이름을 가진 생성자를 매개 변수에 따라 구분하여 정의할 수 있으며 이를 생성자 오버로딩이라고 한다고 배웠었다. 

이처럼 여러 개의 생성자가 사용될 때 하나의 생성자에서 다른 생성자를 호출할 때 `this`를 사용할 수 있다. 

```java
package thisex;

public class Person {
	String name;
    int age;
    
    // 생성자1
    public Person() {
        this("이름 없음", 1); 
    } 
    
    // 생성자2
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
    
    public void showInfo() {
        System.out.println(name + "," + age);
    };
    
    public Person getSelf() {
		return this;
    }
}
```

```java
package thisex;

public class PersonTest {
	public static void main(String[] args) {
        // 생성자1이 생성자2를 호출하여 인스턴스 초기화
        Person personNoname = new Person();
        personNoname.showInfo(); // 이름없음, 1  
        
        personNoname.getSelf(); // personNoname 인스턴스 메모리 출력
    }
}
```

- 참고로 `this`로 다른 생성자를 호출 할 때 그 위에 다른 statement를 작성할 수 없다.

- `getSelf()` 메서드를 실행했을 때 실행되는 `this`는 해당 인스턴스의 메모리 주소를 반환한다!


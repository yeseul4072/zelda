## 상속 - 추상클래스, super, 오버라이딩, 클래스 형변환 

### 추상클래스

> 추상 클래스란 구체적이지 않은 클래스를 의미한다. 

- 클래스 앞에 `abstract` 키워드를 이용해서 정의한다.
- 미완성의 **추상 메소드**를 포함할 수 있다.
  - 추상 메소드란, 내용이 없는 메소드이다.
  - 추상 메소드는 리턴 타입 앞에 `abstract` 키워드를 붙여야 한다.
  - 메소드가 하나라도 추상 메소드인 경우 해당 클래스는 추상 클래스이다.

- 추상 클래스는 인스턴스를 생성할 수 없다.



추상 클래스 정의하기

```java
package javaStudy;

public abstract class Bird {
    // 추상 메소드
    public abstract void sing();
    
    public void fly() {
        System.out.println("날다.");
    }
}
```

추상 클래스를 상속받는 클래스 생성하기

```java
public class Duck extends Bird {
    @Override
    public void sing() {
        System.out.println("꽥!");
    }
}
```

- 추상 클래스를 상속받은 클래스는 **추상 클래스가 갖고 있는 추상 메소드를 반드시 구현**해야 한다. 
- 만약 추상 클래스를 상속받았지만 부모 클래스가 갖고있는 추상 메소드를 구현하지 않았다면 해당 클래스도 추상 클래스가 된다. 

```java
package javaStudy;

public class DuckExam {
    public static void main(String[] args) {
        Duck duck = new Duck();
        duck.sing(); // 꽥!
        duck.fly(); // 날다.
        
        Bird b = new Bird(); // 오류
    }
}
```

- 추상 클래스를 상속받은 Duck 클래스의 인스턴스를 생성하고, 두개의 메소드를 사용할 수 있다.
- 추상 클래스는 부모 클래스로만 사용가능하며 인스턴스를 생성할 수 없다.



### super와 부모생성자

class가 인스턴스화 될 때 **생성자가 실행되면서 객체가 초기화**되는데, 이때 **부모의 생성자 -> 자신의 생성자 순으로 실행**된다.

```java
package javaStudy;

public class Car {
    public Car() {
        System.out.println("Car의 기본 생성자입니다.");
    }
}

public class Bus extends Car {
    public Bus() {
        System.out.prinln("Bus의 기본 생성자입니다.");
    }
}
```

```java
// 생성자 테스트

public class BusExam {
    public static void main(String[] args) {
        Bus b = new Bus(); 
    }
}

// 결과
// Car의 기본 생성자입니다.
// Bus의 기본 생성자입니다.
```

- new 연산자로 Bus 객체를 생성하면, Bus 객체가 메모리에 올라갈 때 부모인 Car 객체도 함께 메모리에 올라간다.

**super**

- 부모 객체를 나타내는 키워드

- `super()` 로 부모의 기본 생성자를 호출할 수 있다. 즉,

```java
public class BusExam {
    public static void main(String[] args) {
        // 아래 구문이 자동으로 실행되는 것이다.
        super();
        Bus b = new Bus(); 
    }
}
```



컴파일러가 `super()` 가 자동으로 실행되어 부모 생성자를 호출하는데 super를 알고 있어야하는 이유가 뭘까? 

1. 부모의 기본 생성자가 아닌 다른 생성자를 호출해야할 때

```java
public class Car {
    public Car(String name) {
        System.out.println(name + " 을 받아들이는 생성자입니다.");
    }
}

public class Bus extends Car {
    // 컴파일 오류!
    //public Bus() {
        //System.out.prinln("Bus의 기본 생성자입니다.");
    //}
    
    public Bus() {
        super("소방차");
        System.out.prinln("Bus의 기본 생성자입니다.");
    }
}
```

```java
public class BusExam {
    public static void main(String[] args) {
        Bus b = new Bus(); 
    }
}
```

- Car 클래스에 기본 생성자가 존재하지 않는 경우 Bus 생성자를 실해하면 컴파일 오류가 발생한다.

2. 자식 클래스에서 부모 클래스의 필드나 메소드를 사용할 때



### 오버라이딩

> 부모가 가지고 있는 메소드와 똑같은 모양의 메소드를 자식이 가지고 있는 것이다. 즉, 자식 클래스에서 부모 클래스의 메소드를 재정의하는 것이다.

```java
//run 메소드를 가지고 있는  Car클래스 
public class Car{
    public void run(){
        System.out.println("Car의 run메소드");
    }
}

//Car 를 상속받는 Bus 클래스 
public class Bus extends Car{

}

public class BusExam{
    public static void main(String args[]){
        Bus bus = new Bus();
        bus.run();  //Car의 run메소드가 실행된다. 
    }
}
```

- 자식 클래스는 부모 클래스가 가진 메소드를 정의하지 않고 사용할 수 있다. 

```java
// Car가 가진 run 메소드를 Bus에서 새로 정의해보자
public class Bus extends Car{
	public void run() {
        System.out.println("Bus의 run메소드");
    }
}

public class BusExam{
    public static void main(String args[]){
        Bus bus = new Bus();
        bus.run();  //Bus의 run메소드가 실행된다. 
    }
}
```

- 메소드를 오버라이드하면, 항상 자식 클래스에서 정의된 메소드가 호출된다.

만약 부모 메소드를 사용하고 싶다면 `super` 를 사용하면 된다.

```java
public class BusExam{
    public static void main(String args[]){
        Bus bus = new Bus();
        super.run(); // Car의 run메소드가 실행된다.
        bus.run();  //Bus의 run메소드가 실행된다. 
    }
}
```



### 클래스 형변환

부모타입으로 자식객체를 참조할 수 있으나, 부모타입으로 자식객체를 참조하게 되면 **부모가 가지고 있는 메소드만 사용**할 수 있다.

```java
public class Car{
    public void run(){
        System.out.println("Car의 run메소드");
    }
}

public class Bus extends Car{
    public void ppangppang(){
        System.out.println("빵빵.");
    }   
}
```

```java
public class BusExam{
    public static void main(String args[]){
        Car car = new Bus();
        car.run();
        car.ppangppang(); // 컴파일 오류 발생        
    }
}
```

- `ppangppang()` 메소드를 호출하고 싶다면 Bus 타입의 참조 변수로 참조해야 한다.

상속관계에 있는 객체들끼리 형변환이 가능하다.

- 부모타입으로 자식타입 객체를 참조할 때는 묵시적으로 형변환이 일어난다.
- 부모타입의 객체를 자식타입으로 참조하게 할때에는 명시적으로 형변환해주어야 한다.

```java
public class BusExam{
    public static void main(String args[]){
        Car car = new Bus(); // Bus -> Car 묵시적 형변환
        car.run();
        
        Bus bus = (Bus)car; // Car -> Bus 명시적 형변환
        bus.run();
        bus.ppangppang();
    }
}
```






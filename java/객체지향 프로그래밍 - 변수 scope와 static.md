## 변수의 스코프와 static

> 변수들은 사용 가능한 범위를 가지며, 그 범위를 변수의 스코프라고 한다.

- 변수가 선언된 블럭이 변수의 사용범위이다. 

```java
package javaStudy;

public class VariableScopeExam {
    int globalScope = 10;
    static int staticValue = 7;
    
    public void scopeTest(int value) {
        int localScope = 20;
        
        // 모든 변수 사용 가능하다
        System.out.println(globalScope);
        System.out.println(localScope);
        System.out.println(value);
    }
    
    public void scopeTest2(int value2) {
        System.out.println(globalScope); // 사용 가능
        System.out.println(localScope); // 사용 불가능 -> 컴파일 에러
        System.out.println(value); // 사용 불가능 -> 컴파일 에러
        System.out.println(value2); // 사용 가능
    }
    
    public static void main(String[] args) {
        System.out.println(globalScope); // 사용 불가능
        System.out.println(localScope); // 사용 불가능
        System.out.println(value); // 사용 불가능
        System.out.println(staticValue); // 사용 가능
        
        // static하지 않은 변수를 사용하기 위해서는 객체를 생성해야한다.
        VariableScopeExam v1 = new VariableScopeExam();
        System.out.println(v1.gloablScope); 
    }
}
```

- main 메소드는 `static` 키워드가 붙은 static 메소드로, `static`이 붙은 경우 클래스 메소드 or 클래스 변수로 클래스가 인스턴스화 하지 않아도 사용할 수 있다.
- **static한 메소드 내에서 static하지 않은 필드는 사용할 수 없다.** 

```java
ValableScopeExam v1 = new ValableScopeExam();
ValableScopeExam v2 = new ValableScopeExam();

v1.golbalScope = 20;
v2.golbalScope = 30;

// 인스턴스는 각각 메모리 공간을 가진다.
System.out.println(v1.golbalScope);  //20 이 출력된다.
System.out.println(v2.golbalScope);  //30이 출력된다.

v1.staticVal = 100;
v2.staticVal = 200; 

// static한 변수는 값을 저장할 수 있는 공간이 하나만 생성되므로 인스턴스가 여러개 생성되어도 하나이다.
System.out.println(v1.statVal);  //20 이 출력된다. 
System.out.println(v2.statVal);  //20 이 출력된다. 
```

- 클래스 변수는 `래퍼런스.변수명` 보다 `클래스명.변수명` 으로 사용하는 것이 바람직하다. 


## 열거형(enum)

- 자바는 열거타입을 이용하여 변수를 선언할 때 변수타입으로 사용할 수 있다.
- JDK5에서 추가되었다. JDK5 이전에는 상수를 열거형 대신 사용했다.

```java
// 상수 이용하는 방법

package javaStudy;

public class EnumExam {
    public static final String MALE="MALE";
    public static final String FEMALE="FEMALE";
    
    public static void main(String[] args) {
        String gender1;
        // gender1에 MALE 혹은 FEMALE 중 하나만 넣고 싶다!
        // 이렇게 되면 MALE, FEMALE이 아닌 값도 들어갈 수 있다. 
        gender1 = EnumExam.MALE;
        genfer1 = EnumExam.FEMALE;
    }
}
```

```java
// 열거형 사용하기
// enum 이름 {값1, 값2, ...;}

package javaStudy;

public class EnumExam {
    public static final String MALE="MALE";
    public static final String FEMALE="FEMALE";
    
    public static void main(String[] args) {
        String gender1;
        // gender1에 MALE 혹은 FEMALE 중 하나만 넣고 싶다!
        // 이렇게 되면 MALE, FEMALE이 아닌 값도 들어갈 수 있다. 
        gender1 = EnumExam.MALE;
        genfer1 = EnumExam.FEMALE;
        
        Gender gender2;
        gender2 = Gender.MALE;
        gender2 = Gender.FEMALE;
        
        gender2 =  "boy"; // 컴파일 에러
        
    }
}

enum Gender {
    MALE, FEMALE;
}
```


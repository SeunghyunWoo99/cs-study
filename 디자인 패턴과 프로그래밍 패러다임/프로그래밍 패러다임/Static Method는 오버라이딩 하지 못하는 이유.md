#### Compile Time vs. RunTime
컴파일 타임

- 개발자가 작성한 소소코드를 기계어 코드로 바꾸는 과정

- JAVA : byte 코드로 바꾸는 과정 (JVM이 이 byte 코드를 이해한다)

 

런타임

- 컴파일 과정을 마친 프로그램이 실행되고 있는 시간

 

#### Static binding vs. Dynamic binidng
정적 바인딩

- 컴파일 타임에 호출될 함수 결정

- 컴파일러가 어떤 메소드를 실행할지 컴파일 타임에 결정

동적 바인딩

- 런타임 때 호출될 함수 결정

 

##### Static 메서드는 왜 오버라이딩이 왜 불가할까
JVM이 메서드를 호출할 때, instance method 의 경우 런타임 시 해당 메서드를 구현하고 있는 실제 객체를 찾아 호출한다.(다형성)

하지만 컴파일러와 JVM 모두 static 메서드에 대해서는 실제 객체를 찾는 작업을 시행하지 않기 때문에, 컴파일 시점에 선언된 타입의 메서드를 호출한다. 그래서 static 메소드에서는 다형성이 적용되지 않는다.

이런 동작때문에 static method를 자식클래스에서 재정의하는 것을 overriding 한다고 하지 않고 hiding 한다고 한다.

 

예시코드
```
class SuperClass {
	public static void staticMethod() {
		System.out.println("SuperClass: inside staticMethod");
	}

	public void instance() {
		System.out.println("SuperClass: inside instanceMethod");
	}
}

public class SubClass extends SuperClass {
    //overriding the static method
    public static void staticMethod() {
        System.out.println("SubClass: inside staticMethod");
    }
    
    public void instance() {
        System.out.println("SubClass: inside instanceMethod");
    }
}

public class TestClass {
    public static void main(String[] args) {
        SuperClass superClass = new SubClass();
        SubClass subClass = new SubClass();

        superClass.staticMethod();
        subClass.staticMethod();

        superClass.instance();
        subClass.instance();
    }
}

// 출력 결과
/*
SuperClass: inside staticMethod
SubClass: inside staticMethod

SubClass: inside instanceMethod
SubClass: inside instanceMethod
*/
 
```

 

 

 

참고

https://hsik0225.github.io/java/2020/12/17/Static-Override/

https://todayscoding.tistory.com/16

https://minni7.tistory.com/32

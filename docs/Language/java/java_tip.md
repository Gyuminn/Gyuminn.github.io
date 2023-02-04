---
layout: default
title: Java로 코드를 작성할 때 알아두면 좋을 팁
parent: Java
grand_parent: Language
nav_order: 2
---

# **Java로 코드를 작성할 때 알아두면 좋을 팁**

{: .bg-purple-000}

---

{: .note}
Java를 배우며 알아두면 좋을 팁들에 대해 정리해보자.

1. <span style="background-color:yellow;  font-weight:700">자바에서는 전역 변수로 데이터를 공유하기 원한다면 singleton 패턴으로 디자인해서 사용</span>하는 것을 권장한다.

   - 객체 지향 프로그래밍에서는 전역 변수 사용을 금기시 함.
   - 그런데 모든 인스턴스가 공유하는 변수를 만들고자 하는 경우? static을 떠올릴 수 있지만 객체 지향은 필요한 부분만 외부에 노출하라고 권장한다.
   - 대부분의 경우 서버는 하나의 인스턴스를 이용해서 멀티 스레드로 클라이언트의 요청을 처리하기 때문에 **하나의 클래스에 대한 인스턴스를 1개만 만드는 것**이 일반적이다.

   ```java
   public class Singleton() {
     // 외부에서 직접 인ㄴ스턴스 생성을 못하도록 생성자의 접근 지정자 변경
     private Singleton() {}

     // 하나의 인스턴스 참조를 저장하기 위한 속성(변수)을 생성
     private static Singleton singleton;

     // 인스턴스의 참조를 리턴하는 메서드
     public static Singleton sharedInstance() {
        if (singleton == null) {
           singleton = new Singleton();
        }
        return singleton;
     }
   }
   ```

2. <span style="background-color:yellow;  font-weight:700">
   클래스 안에 `static { }`를 하고 실행되는 코드를 작성하면 클래스가 메모리에 로드가 될 때 코드를 수행한다.</span>
      - 인스턴스 속성을 사용하는 것은 안됨.
      - static 속성에 초기값을 부여하고자 할 때 주로 이용한다.
      - 프로그램 내에서 맨 처음 한 번만 수행할 내용이 있는 경우도 이 블럭을 이용하면 된다.

3. <span style="background-color:yellow;  font-weight:700">지역 변수를 만들 때 final을 붙일 것이라면 반드시 생성하자마자 초기화를 해야한다.</span>

   - 클래스 안에 만들 때는 대부분의 경우 static과 함께 사용하는데 값을 바꿀 수 없다는 뜻이니 굳이 인스턴스마다 만들 필요가 없기 때문이다.
   - 클래스 안에 만들 때는 생성하자마자 초기화를 해도 되고 생성자에서 초기화해도 된다. 다른 곳에서는 초기화가 되지 않는다.
   - 클래스 안에 만들어지는 final은 대부분 클래스 안의 메서드에서 사용하는 옵션인 경우가 많다.
   - 개발자는 대부분 ENUM을 이용하는데 Java API에서는 호환성 문제 때문에 정수 상수를 주로 이용하며, Snake 표기법으로 작성하는 것이 관례이다.

4. <span style="background-color:yellow;  font-weight:700">클래스 안에 기능 구현이 끝나고 난 후 instance 속성을 사용하지 않는 메서드는 static 메서드로 수정하는 것이 좋다.</span>

   - 메서드는 기본적으로 메모리의 메서드(static) 영역에 하나만 만들어지고 이를 호출해서 사용하므로 코드는 기본적으로 공유가 된다.
   - static 메서드를 사용하는 이유는, static 메서드에서는 instance 속성을 사용할 수 없는데(static 속성과 지역변수만 사용 가능) 인스턴스 생성 없이 메서드를 호출할 수 있기 때문에 메모리 절약이 가능하다.

5. <span style="background-color:yellow;  font-weight:700">매개변수가 여러 개일 경우 순서를 기억해야하기 때문에 클래스를 만들어서 사용하는 것을 권장한다.</span>

   - 클래스 대신에 Map을 사용하는 경우가 있는데 가독성이 떨어지는 부분을 고려해야 한다.

6. <span style="background-color:yellow;  font-weight:700">abstract 메서드를 소유한 class를 extends하거나 interface를 implements하게 되면 반드시 overriding을 해서 내용을 만들어야 한다.</span>

   - 자바에서는 abstract 메서드가 abstract class나 interface에 존재해야 한다.
   - abstract class는 인스턴스를 생성할 수 없는 클래스이다.

7. <span style="background-color:yellow;  font-weight:700">Interface를 사용하는 이유가 다중 상속이라는 것은 절대 틀린 말이다. java는 단일 상속이다.</span>

   - Interface는 상수(static final)과, abstract method와, default method를 소유한 객체이다.
   - 인터페이스에 추상 메서드가 있다면 클래스에서 반드시 구현을 해야 한다.
   - 인터페이스를 implements하게 되면 인터페이스에 있는 메서드가 클래스에 반드시 구현되어있다고 보장할 수 있다.
   - 다형성 구현과, 특정한 메서드가 구현되어있다라는 것을 보장하기 위해서 사용한다.

8. <span style="background-color:yellow;  font-weight:700">Service 클래스는 반드시 Template Method Pattern을 적용해야 한다.</span>

   - Template Method Pattern은 내용을 구현하기 전에 모양을 가진 인터페이스를 만들고 그 인터페이스를 implements해서 구현하는 디자인 패턴이다.
   - 일반적인 데이터베이스 연동 프로젝트를 만들면 `View`, `Controller`, `Service`, `Repository`, `데이터를 표현하기 위한 클래스(DTO, VO, Entity)`와 같이 5가지 종류의 내용을 만들어낸다.
   - Repository도 예전에는 이 패턴을 적용했는데 JPA와 같은 프레임워크를 사용하면 인터페이스만 만들면 내부 구현을 해주기 때문에 최근에는 적용하지 않는다.

9. <span style="background-color:yellow;  font-weight:700">호출하는 메서드에 예외를 처리하도록 하기</span>

   - 메서드의 매개변수 뒤에 `throws 예외처리클래스이름나열`하면 이 메서드를 호출하는 메서드에서 반드시 예외처리클래스에 해당하는 예외를 처리해야 한다. 그렇지 않으면 컴파일 에러가 발생한다.
   - java 애플리케이션의 main 메서드는 운영체제가 호출하는 메서드이다. main메서드에서 throws로 예외를 던지면 예외를 처리할 필요가 없어진다. 학습을 할 때 예외처리를 하는 것이 번거로워서 main 메서드에서 예외를 던지는 경우가 있는데 실제 애플리케이션 개발에서는 권장하지 않는다.

10. <span style="background-color:yellow;  font-weight:700">Java API 문서를 확인할 때는 상속 계층과 구현된 인터페이스를 확인하자.</span>

    - **Field Summary** - static final(클래스 이름으로 호출)로 만들어져 있는데 이 클래스 안에서 사용되는 옵션 값이다.
    - **Contructor** - 생성자.
    - **Method** - 하나씩 설명된 메서드는 자신의 클래스에만 있는 메서드이거나 상속된 메서드 중에서 재정의된 메서드이고 박스에 한꺼번에 나열된 메서드는 상속된 메서드를 그대로 사용한다.

11. <span style="background-color:yellow; font-weight:700">데이터베이스에서 null을 저장할 수 있는 컬럼의 경우 기본 자료형 보다는 Wrapepr Class를 사용하는 것이 좋다.</span>

    - Wrapper Class는 자바의 기본형 데이터를 인스턴스로 생성할 수 있도록 해주는 클래스이다.
    - 자바의 기본형은 참조를 저장하기는 하지만 null을 대입할 수 없는 구조로 만들어져 있다.
    - 기본형과 다른 자료형은 데이터의 의미가 다르기 때문에 형 변환도 불가능하다.
    - 그러나 Wrapper Class는 Object 클래스로부터 상속을 받았기 때문에 인스턴스를 생성해서 Object 클래스 타입의 변수에 대입을 할 수 있고 기본형이 아니기 때문에 null도 저장할 수 있다. 클래스이므로 자신과 관련된 메서드나 속성도 소유할 수 있다.

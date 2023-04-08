# GDSC 과제연

1. 의존과 의존성

우선 의존 관계부터

의존관계는 의존 대상 B가 변하면, 그것이 A에 영향을 미칠 때 A는 B와 의존관계라고 한다.

쉽게 말해 B가 변경되었을 때 그 영향이 A에 미치는 관계를 말한다.

ex> 피자 가게의 요리사는 피자 레시피에 의존한다. 만약 피자 레시피가 변경된다면, 요리사는 피자를 새로운 방법으로 만들게 된다. 레시피의 변화가 요리사에 미쳤기 때문에 **요리사는 레시피에 의존한다**
라고 할 수 있다.

```jsx
public class PizzaChef{
	
	private PizzaRecipe pizzaRecipe;
	
	public PizzaChef() {
		this.pizzaRecipe = new PizzaRecipe();
	}
	
}
```

→ 문제 

1. 피자 쉐프가 레시피에 너무 강하게 결합되어 있음

그러니까 의존관계 주입을 해야한ㄷ.

 **의존 관계 주입(Dependency Injection)**
**어떤 객체가 사용하는 의존 객체를 직접 만들어 사용하는게 아니라, 주입 받아 사용하는 방법(외부에서 결정해주는것이다.** (**new 연산자**
를 이용해서 객체를 생성하는 것이라고 생각하면 된다)

```jsx
import org.springframework.stereotype.Service;

@Service
public class BookService {

    private BookRepository bookRepository;

    public BookService(BookRepository bookRepository) {
        this.bookRepository = bookRepository;
    }
}
```

```jsx
@Service
public class BookRepository {
      // DI Test
}
```

2 . @Autowired 의존성 주입 

@Autowired는 의존성 주입을 할 때 사용하는 Annotation으로 의존 객체의 **타입**에 해당하는 bean을 찾아 주입하는 역할을 한다. 

가능 사용 위치

- 생성자
- Setter
- 필드

예시

```jsx
@Service
public class TestService {

    TestRepository testRepository;
    
    @Autowired
    public TestService(TestRepository testRepository) {
        this.testRepository = testRepository;
    }
}
```

빈이 등록이 되어 있다는게 전제이다. 

 3. DIP 

→ 의존성 역전 원칙 

DIP 원칙이란 객체에서 어떤 Class를 참조해서 사용해야하는 상황이 생긴다면, 그 Class를 직접 참조하는 것이 아니라 그 **대상의 상위 요소(추상 클래스 or 인터페이스)로 참조**하라는 원칙이다.

객체들이 서로 정보를 주고 받을 때는 의존 관계가 형성되는데, 이 때 객체들은 **나름대로의 원칙**을 갖고 정보를 주고 받아야 하는 약속이 있다. 여기서 나름대로의 원칙이란 추상성이 낮은 클래스보다 **추상성이 높은 클래스와 통신**을 한다는 것을 의미하는데 이것이 DIP 원칙이다.

다시 말하면 클라이언트(사용자)가 상속 관계로 이루어진 모듈을 가져다 사용할때, 하위 모듈을 **직접 인스턴스를 가져다 쓰지 말라**
는 뜻이다. 왜냐하면 그렇게 할 경우, 하위 모듈의 구체적인 내용에 클라이언트가 의존하게 되어 하위 모듈에 변화가 있을 때마다 **클라이언트나 상위 모듈의 코드를 자주 수정**
해야 되기 때문이다.

ex→>>

대표적으로 컬렉션 프레임워크를 들수 있는데, 보통 ArrayList 나 HashSet 자료형을 인스턴스화 할때 변수 타입을 ArrayList, HashSet 같은 구체 클래스 타입으로 선언하는 것이 아닌, List 나 Set 같은 인터페이스 타입으로 선언하는 것을 봐왔을 것이다.

이것도 DIP 원칙을 따른 코드 선언이라고 봐도 무방하다.

```jsx
List<String> myList = new ArrayList()<>;
    
Set<String> mySet = new HashSet()<>;

Map<int, String> myMap = new HashMap()<>;
```

 4. 스프링 빈과 스프링 컨테이너

스프링 빈이란 스프링 IOC 컨테이너에서 관리하는 자바객체입니다. 

우리가 알던 기존의 Java Programming 에서는 Class를 생성하고 new를 입력하여 원하는 객체를 직접 생성한 후에 사용했었습니다. 하지만 Spring에서는 직접 new를 이용하여 생성한 객체가 아니라, Spring에 의하여 관리당하는 자바 객체를 사용합니다. 이렇게 **Spring에 의하여 생성되고 관리되는 자바 객체를 Bean**
이라고 합니다. Spring Framework 에서는 Spring Bean 을 얻기 위하여 ApplicationContext.getBean() 와 같은 메소드를 사용하여 Spring 에서 직접 자바 객체를 얻어서 사용합니다.

스프링 컨테이너는 위의 빈의 생명 주기를 관리하며, 생성된 자바 객체들에게 추가적인 기능을 제공하는 역할을 합니다. 

스프링 컨테이너 종류 

스프링 컨테이너는 BeanFactory와 ApplicationContext가 있습니다.

스프링 빈을 컨테이너에 등록하는 방법

bean configuration file에 직접 등록하는 방식 

```jsx
// Hello.java
@Configuration
public class HelloConfiguration {
    @Bean
    public HelloController sampleController() {
        return new SampleController;
    }
}
```

 5. Jdbc와 jpa

 편해지는 단계

jdbc→ jdbc template 이용하기 → jpa 사용하기 

jdbc란 자바 프로그램이 데이터베이스와 연결되어 데이터를 주고 받을 수 있게 해주는 프로그래밍 인터페이스이다.o;

- 응용프로그램과 dbms간의 통신을 중간에서 번역해주는 역할을 한다.

jdbc프로그램은 네트워크를 통해서 데이터베이스와 연결을 맺고, SQL을 전달해서 데이터베이스가 이를 실행하는 흐름이기 때문에 다음과 같은 순서대로 프로그램을 작성해야만한다.

1) 네트워크를 통해서 데이터베이스를 연결을 맺는 단계

2) 데이터베이스에 보낼 SQL을 작성하고 전송하는 단계

3) 필요하다면 데이터베이스가 보낸 결과를 받아서 처리하는 단계

4) 데이터베이스와 연결을 종료하는 단계

JPA 란DB 테이블과 객체 사이의 매핑을 처리해주는 ORM이란 기술의 표준이다.

그렇다면 ORM은 또 무엇일까?

ORM 이란, Object-relation mapping(객체 관계 매핑) 으로 객체는 객체대로, 관계형 DB는 DB 대로 설계하고

그 사이에서 ORM 이 매핑해주는 기술이다.

![Untitled](GDSC%20%E1%84%80%E1%85%AA%E1%84%8C%E1%85%A6%E1%84%8B%E1%85%A7%E1%86%AB%202df7d066818646fc977ca70a2d0fbd88/Untitled.png)

 -JPA는 기존의 반복 코드는 물론이고, 기본적인 SQL도 JPA가 직접 만들어서 실행해준다.
 -JPA를 사용하면, SQL과 데이터 중심의 설계에서 객체 중심의 설계로 패러다임을 전환을 할 수 있다.
 -JPA를 사용하면 개발 생산성을 크게 높일 수 있다.
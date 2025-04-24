# Toby Spring

## 자동 구성 기반 애플리케이션(@Autoconfiguration)

스프링 부트가 어떻게 개발을 빠르게 할 수 있도록 하는가?

### 메타 애노테이션과 합성 애노테이션

메타 애노테이션을 통해서 기존 기능 + 명시 효과 + 새로운 기능 추가

애노테이션은 상속의 개념은 없다.

```java
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.METHOD)
@UnitTest
@interface FastUnitTest {

}

@Retention(RetentionPolicy.RUNTIME)
// annotation_type을 지정해줘야 다른 어노테이션에서 이 어노테이션을 이용할 수 있다
@Target({ElementType.ANNOTATION_TYPE, ElementType.METHOD})
@Test
@interface UnitTest {

}

public class HelloServiceTest {

    @UnitTest
    void simpleHelloService() {
        SimpleHelloService helloService = new SimpleHelloService();

        String ret = helloService.sayHello("Test");

        assertThat(ret).isEqualTo("Hello Test");
    }

    @Test
    void helloDecorator() {
        HelloDecorator decorator = new HelloDecorator(name -> name);

        String ret = decorator.sayHello("Test");

        assertThat(ret).isEqualTo("*Test*");
    }
}
```

### 합성 애노테이션의 적용

RetentionPolicy.RUNTIME으로 지정하는 이유

`기본적인 RententionPolicy는 RetentionPolicy.CLASS인데, 컴파일 된 Class파일까지는 살아있지만, 런타임 시점에 메모리에 로딩될 때 애노테이션 정보가 사라진다.`

### 빈 오브젝트의 역할과 구분

컨테이너 인프라스트럭쳐 빈 → 스프링 컨테이너 자체의 동작을 지원하기 위해 내부적으로 등록되는 빈

애플리케이션 로직 빈 / 애플리케이션 인프라스트럭쳐 빈 / 컨테이너 인프라스트럭쳐 빈

애플리케이션 인프라스트럭쳐 빈 ⇒ 기술과 관련된 빈(DataSource, JpaEntityManager Factory 등)

사용자 구성 정보(ComponentScan) / 자동 구성정보(AutoConfiguration)

자동 구성 정보 ⇒ 인프라 스트럭쳐 빈을 담은 Configuration을 만들어서 적용한다. 

### 인프라 빈 구성 정보의 분리

AutoConfiguration : 만들어진 Configuration이 필요한 경우 스프링이 자동으로 선택한다.

메타 애노테이션을 통해서 인프라 스트럭쳐 빈과 Application 로직 빈을 분리함

![image.png](attachment:5ee62714-e0c2-42ef-b3e5-c08943b58e30:95fb8ded-3e23-406b-be02-7eaca165bc5b.png)

### 동적인 자동 구성 정보 등록

동적으로 가져오려면 ImportSelector를 사용해야 한다.

### 자동 구성 정보 파일 분리

### 자동 구성 애노테이션 적용

![image.png](attachment:33ce58b9-5d81-48a9-a9ba-e22c6f4f89f7:image.png)

### @Configuration과 proxyBeanMethods
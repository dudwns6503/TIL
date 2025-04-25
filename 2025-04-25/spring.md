# Toby Spring

## 조건부 자동 구성

### 스타터와 Jetty 서버 구성 추가

스프링 부트가 제공하는 AutoConfiguration.imports에 100개가 넘는 Configuration 클래스 목록들이 적혀있는데, 각각에 최소 1~2개에 @Bean 메서드가 있다면, 실행 시점에 매번 최소 100개가 넘는 Bean이 등록된다는 얘기인데, 사실은 이렇게 동작하진 않음.

‘조건’을 통해서 생성할 Bean을 선별함.

### @Conditional과 Condition

@Conditional을 붙여서 파라미터로 Condition을 구현하는 클래스를 넘겨줘서 matches를 overriding해서 true일 경우 빈으로 등록, false인 경우 빈으로 등록하지 않는다.

만약 @Configuration 클래스 레벨에 @Conditional이 False이고, @Bean에 붙은 @Conditional은 True라면 Bean은 등록이 될까? ⇒ 안 된다.

### @Conditional 학습 테스트

@BooleanConditional 어노테이션을 만들고 내부에 boolean 형 value()를 가지게 한다. Condition을 구현하는 BooleanCondition을 만든 후 아래와 같이 matches를 오버라이딩 한다.

```java
private static class BooleanCondition implements Condition {
        @Override
        public boolean matches(ConditionContext context, AnnotatedTypeMetadata metadata) {
            Map<String, Object> annotationAttributes = metadata.getAnnotationAttributes(BooleanConditional.class.getName());
            Boolean value = (Boolean) annotationAttributes.get("value");
            return value;
        }
    }
```

### 커스톰 @Conditional

라이브러리를 읽어서, 특정 클래스가 존재할 경우에 Bean을 등록하는 Condition을 만들어보자!

```java
@MyAutoConfiguration
@Conditional(TomcatWebServerConfig.TomcatCondition.class)
public class TomcatWebServerConfig {
    ...
    
    static class TomcatCondition implements Condition {
        @Override
        public boolean matches(ConditionContext context, AnnotatedTypeMetadata metadata) {
            return ClassUtils.isPresent("org.apache.catalina.startup.Tomcat", context.getClassLoader());
        }
    }
}
```

 @ConditionalOnMyClass(”org.apache.catalina.startup.Tomcat”) 을 통해서 빈 등록 여부를 결정하는 어노테이션 만들기

```java
// @ConditionalOnMyClass
@Retention(RetentionPolicy.RUNTIME)
@Target({ElementType.TYPE, ElementType.METHOD})
@Conditional(OnMyClassCondition.class)
public @interface ConditionalOnMyClass {
    String value();
}

// OnMyClassCondition.class
public class OnMyClassCondition implements Condition {
    @Override
    public boolean matches(ConditionContext context, AnnotatedTypeMetadata metadata) {
        Map<String, Object> attrs = metadata.getAnnotationAttributes(ConditionalOnMyClass.class.getName());
        String value = (String) attrs.get("value");
        return ClassUtils.isPresent(value, context.getClassLoader());
    }
}

```

### 자동 구성 정보 대체하기

@ConditionalOnMissingBean(스프링 부트에서 이미 사용하고 있는 어노테이션) 을 통해서 해당 타입의 Bean이 등록되어 있지 않다면 등록하게 함. 여기서는 이미 사용자가 WebServerConfiguration을 통해서 같은 타입의 Bean을 등록했기 때문에 아래 코드에서 Bean이 생성되서 등록되지 않음.

!! 사용자가 등록한 Bean이 먼저 등록된다(DeferredImportSelector) !!

```java
@MyAutoConfiguration
@ConditionalOnMyClass("org.apache.catalina.startup.Tomcat")
public class TomcatWebServerConfig {
    @Bean(name = "tomcatWebServerFactory")
    @ConditionalOnMissingBean
    public ServletWebServerFactory servletWebServerFactory() {
        return new TomcatServletWebServerFactory();
    }
}
```

### 스프링 부트의 @Conditional

@ConditionalOnClass

@ConditionalOnMissingClass

@ConditionalOnBean

@ConditionalOnMissingBean
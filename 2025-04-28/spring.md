# Toby Spring

## 외부 설정을 이용한 자동 구성

### Environment 추상화와 프로퍼티

### 자동 구성에 Environment 프로퍼티 적용

우선순위

SystemProperty > EnvironmentProperty > ApplicationProperty

```java
@MyAutoConfiguration
@ConditionalOnMyClass("org.apache.catalina.startup.Tomcat")
public class TomcatWebServerConfig {
    @Bean(name = "tomcatWebServerFactory")
    @ConditionalOnMissingBean
    public ServletWebServerFactory servletWebServerFactory(Environment env) {
        TomcatServletWebServerFactory factory = new TomcatServletWebServerFactory();
        factory.setContextPath(env.getProperty("contextPath"));
        return factory;
    }
}

// application.properties
contextPath=/app
```

### @Value와 PropertySourcesPlaceholderConfigurer

```java
@MyAutoConfiguration
@ConditionalOnMyClass("org.apache.catalina.startup.Tomcat")
public class TomcatWebServerConfig {

    @Value("${contextPath}")
    String contextPath;

    @Bean(name = "tomcatWebServerFactory")
    @ConditionalOnMissingBean
    public ServletWebServerFactory servletWebServerFactory() {
        TomcatServletWebServerFactory factory = new TomcatServletWebServerFactory();
        factory.setContextPath(this.contextPath);
        return factory;
    }
}

// 자동 구성정보 추가
@MyAutoConfiguration
public class PropertyPlaceholderConfig {
    @Bean
    PropertySourcesPlaceholderConfigurer propertySourcesPlaceholderConfigurer() {
        return new PropertySourcesPlaceholderConfigurer();
    }
}

//tobyspring.config.MyAutoConfiguration.imports
tobyspring.config.autoconfig.PropertyPlaceholderConfig
```

### 프로퍼티 클래스의 분리

### 프로퍼티 빈의 후처리기 도입
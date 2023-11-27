> [Primary Goal Of SpringBoot](https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/#getting-started.introducing-spring-boot)
> 1. 모든 스프링 개발을 위해 <b>매우 빠르고 폭넓게 액세스 할 수 있는 시작 경험을 제공</b>해줍니다.
> 2. 설정을 일일이 설정하지 않아도 <b>설정을 제공</b>해 줍니다 하지만 사용자가 원하는 대로 설정을 쉽고 빠르게 변경 가능합니다.
> 3. 많은 종류의 프로젝트(예: 내장형 서버, 보안, 메트릭, 상태 점검 및 외부 구성)에 공통적으로 사용되는 다양한 <b>비기능적 기능을 제공</b>합니다.
> 4. 코드 생성도 없고 <b>XML 구성도 필요하지 않습니다.</b>

<br>

> <b> ✋ 들어가기에 앞서,</b>    
> 자동으로 등록된 빈들이 <u>언제 어떻게 등록</u>하게 된 것인지 알아야 하는 경우를 대비하여   
> <b>대략적으로 어떻게 동작하는지 정도</b>만 이해하면 될 듯

<br>


# 스프링부트 자동 구성
- 스프링부트의 자동 환경 구성은 스프링부트의 <b>대표적인 기능</b>으로 볼 수 있음   
- `AOP`, `web`, `jdbc`, `jpa`, `redis`, `security` 등 수많은 자동 환경 구성을 제공

## 사용 방법
`@EnableAutoConfiguration` 혹은 [`@SpringBootApplication`](#springbootapplication) 어노테이션을 `@Configuration` 클래스에 추가하여 Auto-configuration 사용 가능

> :bulb: 이때 `@EnableAutoConfiguration` , `@SpringBootApplication` <b>둘 중 하나</b>만 추가 !!!

```
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class TestApplication {

	public static void main(String[] args) {
		SpringApplication.run(TestApplication.class, args);
	}

}
```
<br>

## 자동 구성 비활성화
`@SpringBootApplication` 혹은 `@EnableAutoConfiguration` 어노테이션에 `exclude` 속성을 통해 비활성화 가능

```
@SpringBootApplication(exclude = { DataSourceAutoConfiguration.class })
public class MyApplication {

}
```

<br>

## @SpringBootApplication
> :bulb: 이 어노테이션은 다음 세가지 어노테이션을 합친 형태

- `@EnableAutoConfiguration` : SpringBoot의 auto-configuration 메커니즘 활성화
- `@ComponentScan` : `@Component` 어노테이션이 붙은 파일 스캔
- `@SpringBootConfiguration` : 기타 추가적인 빈들 등록 및 클래스 추가 (`@Configuration` 대안)

```
// Same as @SpringBootConfiguration @EnableAutoConfiguration @ComponentScan
@SpringBootApplication
public class MyApplication {

    public static void main(String[] args) {
        SpringApplication.run(MyApplication.class, args);
    }

}
```

<br>

## 동작 원리
> :bulb: [`spring.factories`](https://github.com/spring-projects/spring-boot/blob/main/spring-boot-project/spring-boot-autoconfigure/src/main/resources/META-INF/spring.factories) 파일에 선언된 `XXXConfiguration`들이 모두 자동 설정 대상에 해당

1. `@SpringBootApplication`
2. `@EnableAutoConfiguration`
3. `@Import(AutoConfigurationImportSelector.class)`
4. `resources/META-INF/spring/org.springframework.boot.autoconfigure.AutoConfiguration.imports` 파일을 열어, 설정 정보 선택
5. 선택된 설정 정보가 스프링 컨테이너에 등록되고 사용

<br>

# :question: 예상 질문
없을 것 같습니다..


# :newspaper: Reference
- [[spring-boot docs] : 6.4 Auto-Configuration](https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/#using.auto-configuration)
- [스프링부트의 AutoConfiguration 원리](https://donghyeon.dev/spring/2020/08/01/%EC%8A%A4%ED%94%84%EB%A7%81%EB%B6%80%ED%8A%B8%EC%9D%98-AutoConfiguration%EC%9D%98-%EC%9B%90%EB%A6%AC-%EB%B0%8F-%EB%A7%8C%EB%93%A4%EC%96%B4-%EB%B3%B4%EA%B8%B0/)   
- [스프링부트 AutoConfiguration 동작 원리 파헤치기](https://wildeveloperetrain.tistory.com/292)
- [스프링부트 자동설정](https://zion830.tistory.com/112)
- [스프링부트 핵심기능 자동설정](https://hanseom.tistory.com/333)
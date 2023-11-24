# Springboot 라이브러리 관리

## Springboot 라이브러리 관리
"웹 프로젝트를 하나 만들기 위해 Spring Web, Tomcat, JSON Pasing, Logger 등 수 많은 라이브러리들이 필요하며, 이 라이브러리들의 버전까지 선택해야한다. 또한 이 라이브러리들 간의 호환성 또한 고려해야하는 것이 기존 스프링 프레임워크에서 불편한 점이었다."
<br/>

😊스프링 부트는 개발자가 라이브러리를 편리하게 사용하여 개발을 할 수 있도록 다양한 기능을 제공한다.😊
<br/>

## 스프링 부트 라이브러리 버전 관리
 - 스프링 부트는 수 많은 라이브러리의 버전을 직접 관리해줍니다. 
 - 버전 관리 기능을 사용하려면 io.spring.dependency-management 플러그인을 사용해야 합니다.  

### 스프링 부트가 관리하는 외부 라이브러리 버전을 확인하는 방법
[스프링 공식 문서](https://docs.spring.io/spring-boot/docs/current/reference/html/dependency-versions.html#appendix.dependency-versions.coordinates)

## 스프링 부트 스타터
스프링 부트 스타터는 사용하기 편리하게 의존성을 모아둔 세트.
> spring-boot-starter : 핵심 스타터, 자동 구성, 로깅, YAML
> spring-boot-starter-jdbc : JDBC, HikariCP 커넥션풀
> spring-boot-starter-data-jpa : 스프링 데이터 JPA, 하이버네이트
> spring-boot-starter-data-redis : 스프링 데이터 Redis, Lettuce 클라이언트
> spring-boot-starter-web : 웹 구축을 위한 스타터, RESTful, 스프링 MVC, 내장 톰캣
> 등등
<br/>

[공식문서 - 스프링 부트 스타터 전체목록](https://docs.spring.io/spring-boot/docs/current/reference/html/using.html#using.build-systems.starters) 



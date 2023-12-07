# 스프링과 스프링 부트

## Spring Boot이 Spring과 다른 점

### 1. 내장 톰캣 (Embed Tomcat)
스프링 부트 내부에 Tomcat이 포함되어있기 때문에 따로 Tomcat을 설치하거나 버전을 관리해야하는 수고를 덜 수 있다.  
[스프링부트의 내장 톰캣(WAS)](./springboot_was.md)  

### 2. starter를 통한 dependency 자동화
spring-boot-starter가 대부분의 dependency를 관리해주어서 호환되는 버전을 관리에 힘을 쏟을 필요가 없다.  
starter 가 알아서 필요한 라이브러리들을 받아오기 때문에 일일이 설정할 필요없음.  

### 3. XML 설정을 하지 않아도 된다. 👉 자동 구성(Auto Configuration)  
<br/>

### 4. jar 파일을 이용해 쉬운 배포 가능  
<br/>
<br/>


# :question: 예상 질문
<details>
  <summary><b>스프링이 아닌 스프링 부트를 사용하신 이유가 뭔가요?</b></summary>
  <div markdown="1">
  스프링부트는 스프링보다 설정함에 있어서 편리해서 사용했습니다. stater를 통해 dependency 관리가 편리하고 xml 설정을 하지 않아도 되서 사용했습니다.
  </div>
</details>
<br>

# :newspaper: Reference

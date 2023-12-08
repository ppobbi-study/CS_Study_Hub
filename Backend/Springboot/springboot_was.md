# 스프링부트 내장 톰캣 (WAS)  
  
" 이전에는 웹 어플리케이션을 구동하고 싶으면 웹 어플리케이션 서버(WAS)를 별도로 설치하고, 웹 어플리케이션 빌드파일(WAR)을 배포해야 했다. "  
  

## WAR 배포 방식의 단점
- 톰캣과 같은 WAS를 별도로 설치해야 함
- 개발 환경 설정이 복잡함
- 배포 과정이 복잡함
- 톰캣 버전을 변경하려면 톰캣을 다시 설치해야함  

<br/>
"이러한 문제를 해결하기 위해 톰캣을 라이브러리로 제공하는 내장 톰캣(embed tomcat) 기능을 제공한다."  
<br/>
  
## 외장 서버 vs 내장 서버
[![](./images/springboot_img3.PNG?width=400px)]()  
  
🎈 **외장 서버** : 웹 애플리케이션 서버에 WAR 파일을 배포하는 방식으로 WAS를 실행해서 동작  
🎈 **내장 서버** : 애플리케이션 JAR안에 다양한 라이브러리들과 WAS 라이브러리가 포함되는 방식으로 main() 메서드를 실행해서 동작  
  

## 스프링 부트와 웹 서버
스프링 부트는 내장 톰캣을 사용해서 빌드와 배포를 편리하게 해주며, 빌드 할 때 하나의 JAR를 사용한다. `spring-boot-starter-web`를 사용하면 내부에서 내장 톰캣을 사용한다. 라이브러리 의존 관계를 따라가면 내장 톰캣(tomcat-embed-core)이 포함된 것을 확인할 수 있다.  
[![](./images/springboot_img4.PNG?width=400px)]()  
  
## 스프링 부트와 웹 서버 실행 과정
[![](./images/springboot_img5.PNG?width=400px)]()  
  
@SpringBootApplication 어노테이션이 있는 자바 main()메서드를 호출해서 실행한다.  
1. 스프링 컨테이너 생성
2. WAS(내장 톰캣) 생성  
<br/>
[![](./images/springboot_img6.PNG?width=400px)]() 

## 스프링 부트와 웹서버 빌드 및 배포
- 내장 톰캣이 포함된 스프링 부트를 빌드하면 build/libs/dangdangranger-0.0.1-SNAPSHOT.jar 파일이 만들어진다.
- 여기서 plain.jar 파일은 우리가 개발한 코드만 순수하게 jar로 빌드한 것이다.
[![](./images/springboot_img7.PNG?width=400px)]()  

<br/>

# :question: 예상 질문
<details>
  <summary><b>스프링 부트의 내장 was에 대해서 설명해주세요</b></summary>
  <div markdown="1">
  설명해보쇼.
  </div>
</details>
<br>

# :newspaper: Reference
[내장 톰캣](https://hanseom.tistory.com/331)
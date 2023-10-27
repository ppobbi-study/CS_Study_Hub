# JVM(Java Virtual Machine)

> **자바프로그램 실행을 위한 소프트웨어**

## 왜 사용할까?
> **"write once, run everywhere"**
- 자바는 하나의 바이트 코드(.class)로 플랫폼에 상관없이 실행이 가능하다.
    - .class 파일 - .자바 소스 코드(.java)를 컴파일한 결과물

- 자바는 플랫폼에 비종속적, but JVM은 플랫폼에 종속적
    - C의 경우, 플랫폼에 맞는 각각의 컴파일러가 필요
    - Java의 경우, 하나의 자바 컴파일러가 변환한 바이트 코드를 실행할 각각의 JVM이 필요

<p align="center" width="100%">
    <img src="https://github.com/ppobbi-study/CS_Study_Hub/blob/geon/SelfStudy/%EB%82%98%EA%B1%B4/Java/img/compile_c.png" width="49%">
    <img src="https://github.com/ppobbi-study/CS_Study_Hub/blob/geon/SelfStudy/%EB%82%98%EA%B1%B4/Java/img/compile_java.png" width="49%">
</p>

## 단점은?
- 두 번의 변환과정으로 인해 속도 문제가 발생
    - 자바 컴파일러 : .java -> .class
    - JVM : .class -> 기계어 파일(Native Code)

## 어떻게 동작할까?
> Interpreter와 JIT 방식을 적절히 혼합해 사용

### Interpreter 방식
-  한 줄 씩 바이트코드를 읽어서 기계어로 컴파일 후 실행

### JIT 방식
- 중복되는 부분의 기계어 코드를 캐싱 후 재사용

### 더 알아보기
[프로그램 실행 방식](https://github.com/ppobbi-study/CS_Study_Hub/blob/geon/SelfStudy/%EB%82%98%EA%B1%B4/Java/ProgrammingBase/program_structure.md)

<br>

## JVM의 구조
![JVM structure](https://github.com/ppobbi-study/CS_Study_Hub/blob/geon/SelfStudy/%EB%82%98%EA%B1%B4/Java/img/JVM_structure.png)

<br>

## JDK vs JRE vs JVM
![JDK structure]https://github.com/ppobbi-study/CS_Study_Hub/blob/geon/SelfStudy/%EB%82%98%EA%B1%B4/Java/img/JDK_structure.png()

### JDK(Java Development Kit)
> 자바로 개발하는데 필요한 SDK
- SDK(Software Development Kit) - 하드웨어 플랫폼, 운영체제 또는 프로그래밍 언어 제작사가 제공하는 소프트웨어 개발 도구
    - 안드로이드 스튜디오 등..

### JRE(Java Runtime Environment)
> JVM + 라이브러리
- 자바로 개발하려면 JDK가 필요하고, 자바를 실행하려면 JRE가 필요하다.

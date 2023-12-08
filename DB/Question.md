# 신입 개발자 기술 면접 질문 정리

## 목차

[👍데이터베이스 특징](#💡-데이터-베이스의-특징에-대해-설명해주세요)

👍[데이터베이스 언어](#💡데이터-베이스-언어ddl-dml-dcl에-대해-설명해주세요)

[👍 쿼리 수행 순서](#💡select-쿼리의-수행-순서를-알려주세요)

[👍 트리거](#💡트리거trigger에-대해-설명해주세요)

[👍 인덱스](#💡index에-대해-설명해주시고-장단점에-대해-아는대로-말해주세요)

[👍 인덱스 자료구조](#💡그렇다면-dbms는-index를-어떻게-관리하고-있나요-index-자료구조)

[👍 정규화](#💡정규화에-대해-설명해주세요)

[👍 정규화 장점](#💡정규화에는-어떤-장점이-있고-어떤-단점이-있는지-아는대로-설명해주세요)

[👍 역정규화](#💡-역정규화를-하는-이유에-대해-아는대로-설명해주세요)

[📰 Reference](#reference)

---

## 💡데이터 베이스의 특징에 대해 설명해주세요.

<details>
  <summary><b>데이터 베이스란?</b></summary>
  <div markdown="1">

사용자가 `공유` 가능하도록 `통합`해서 `저장`해 `운영`하는 데이터 집합
  </div>
</details>


<details>
  <summary><b>데이터 베이스의 특징</b></summary>
  <div markdown="1">

### 실시간 접근성(Real-Time Accessibility)
비정형적인 질의(조회)에 대하여 실시간 처리에 의한 응답이 가능해야 함

### 지속적인 변화(Continuous Evloution) 
새로운 데이터의 삽입(Insert), 삭제(Delete), 갱신(Update)으로 항상 최신의 데이터를 유지해야 함

### 동시 공유(Concurrent Sharing) 
데이터베이스는 서로 다른 목적을 가진 여러 응용자들을 위한 것이므로 다수의 사용자가 동시에 같은 내용의 데이터를 이용해야 함

### 내용 기반 참조(Content Reference)
사용자가 데이터를 요구할 때, 데이터의 주소, 위치가 아닌  데이터 내용으로 찾아야 함


<br>

참고자료: [데이터베이스](https://ko.wikipedia.org/wiki/%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4)
  </div>
</details>



## 💡데이터 베이스 언어(DDL, DML, DCL)에 대해 설명해주세요.

<details>
  <summary><b>DDL, DML, DCL</b></summary>
  <div markdown="1">

### DDL (정의어 : Data Definition Language)
데이터베이스의 구조를 정의

- alter : 테이블 수정
- create : 테이블 생성
- drop : 테이블 삭제
- truncate: 테이블 초기화


### DML (조작어 : Data Manipulation Language) 
데이터베이스를 조작

- select : 데이터 조회
- insert : 데이터 삽입
- update : 데이터 수정
- delete : 데이터 삭제

### DCL (제어어 : Data Control Language) 
데이터베이스 접근, 권한 부여

- grant : 수행 권한 부여 
- revoke : 수행 권한 회수
- commit : 작업 확정
- rollback : 작업 취소, 복구

<details>
<summary>commit과 rollback의 차이가 뭐죠?</summary>
<div>

### Commit
모든 작업을 정상적으로 처리하겠다고 확정하는 명령어

- 변경된 내용을 모두 영구 저장
- 하나의 트랜잭션 과정을 종료

![Alt text](https://wikidocs.net/images/page/4096/1.PNG)


### Rollback
작업 중 문제가 발생했을 때, 트랜잭션 처리 과정에서 발생한 변경 사항을 취소하고 트랜잭션을 종료

- 하나의 묶음 처리가 시작되기 이전 상태로 되돌림

![text](https://wikidocs.net/images/page/4096/2.PNG)

참고 자료: [commit과 rollback 차이(oracle)](https://wikidocs.net/4096)
</div>
<details>
  </div>
</details>

## 💡SELECT 쿼리의 수행 순서를 알려주세요.

<details>
  <summary><b>쿼리 수행 순서</b></summary>
  <div markdown="1">

실행 순서를 모르면, 쿼리를 제대로 작성하기 어려움

![ㅇ](https://i.imgur.com/MtBZDYV.png)


### FROM, ON, JOIN > WHERE, GROUP BY, HAVING > SELECT > DISTINCT > ORDER BY > LIMIT

### 1. FROM
가장 첫 번째로 FROM 절이 실행. 여기서 조회 테이블을 확인하고 테이블의 모든 데이터를 가지고 옴

### 2. ON
조인 조건을 확인

### 3. JOIN
조인 조건에 맞는 테이블과 테이블을 조인(병합)

### 4. WHERE
FROM 절에서 가지고온 데이터 중에서 조건에 일치하는 데이터만 가져옴

### 5. GROUP BY
WHERE 절에서 추려낸 데이터를 가지고 선택한 칼럼으로 그룹화

### 6. HAVING
GROUP BY 절로 그룹화 된 이후에 WHERE 절 처럼 조건에 일치하는 데이터만 가져옴

### 7. SELECT
최종적으로 추려낸 데이터 중에서 어떤 칼럼들을 출력할 것인지 선택
- 만약 distinct가 있다면, select 후 distinct 실행

### 8. ORDER BY
데이터의 순서를 정렬

<br>

참고 자료: [쿼리 순서 ](https://mellowresearch.com/Computer+Science/%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4/SQL+SELECT+%EB%AC%B8+%EC%8B%A4%ED%96%89%EC%88%9C%EC%84%9C+%EC%A0%95%EB%A6%AC)
  </div>
</details>

##  💡트리거(Trigger)에 대해 설명해주세요.

<details>
  <summary><b>트리거</b></summary>
  <div markdown="1">
테이블에 대한 이벤트가 발생했을 때(DML(insert, delete, update) 문이 수행), 데이터베이스에서 자동으로 동작하도록 작성된 프로그램

- 데이터의 상태의 관리를 자동화

<details>
  <summary><b>트리거 장점</b></summary>
  <div markdown="1">

- 데이터 무결성 강화 (참조 무결성)
- 업무 규칙의 설정
- 검사 기능의 확장
  </div>
</details>

참고자료 : [트리거](https://ko.wikipedia.org/wiki/%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4_%ED%8A%B8%EB%A6%AC%EA%B1%B0)


  </div>
</details>

## 💡Index에 대해 설명해주시고, 장/단점에 대해 아는대로 말해주세요.

<details>
  <summary><b>Index</b></summary>
  <div markdown="1">
Index란 테이블을 처음부터 끝까지 검색하는 방법인 FTS(Full Table Scan)과는 달리 인덱스를 검색하여 해당 자료의 테이블을 access 할 수 있는 방법

- 인덱스는 항상 정렬된 상태를 유지하기 때문에 원하는 값을 검색하는데 빠르지만, 새로운 값을 추가하거나 삭제, 수정하는 경우에는 쿼리문 실행 속도가 느려짐

- 즉, 인덱스는 데이터의 저장 성능을 희생하고 그대신 데이터의 검색 속도를 높이는 기능


  </div>
</details>

## 💡그렇다면 DBMS는 Index를 어떻게 관리하고 있나요? (Index 자료구조)


<details>
  <summary><b>자료 구조</b></summary>
  <div markdown="1">

  ### B+ Tree 인덱스 자료 구조
  - 자식 노드가 2개 이상인 B-Tree를 개선 시킨 자료 구조
  - BTree 리프노드들을 LinkedList로 연결해 순차 검색을 용이하게 함
  - 해시 테이블보다 나쁜 O(Log2N)의 시간 복잡도이지만, 일반적으로 사용

  ### 해시 테이블
  - 컬럼의 값으로 생성된 해시를 기반으로 인덱스 구현
  - 시간복잡도가 O(1)이라 검색이 매우 빠름
  - 부등호와 같은 연속적인 데이터를 위한 순차 검색이 불가능하기 때문에 범위 검색은 적합하지 않음
  - 주로 등가검색(특정 값에 대한 검색)에 사용

  ### R-tree 인덱스 자료구조
  - 공간적 데이터를 위해 설계된 인덱스
  - 다차원 객체를 저장하고 검색하는 데 사용
  - 보통 좌표, 거리, 지역의 윤곽선 등 저장해 해당 객체를 더빠르게 쿼리하는 목적으로 사용

  <details>
  <summary><b>R-tree</b></summary>
  <div markdown="1">

![rtree](https://upload.wikimedia.org/wikipedia/commons/thumb/5/57/RTree-Visualization-3D.svg/600px-RTree-Visualization-3D.svg.png)
  ### R 트리란?
  R-트리는 공간적 접근 방법 , 즉 지리적 좌표 , 직사각형 또는 다각형 과 같은 다차원 정보를 색인화하는 데 사용되는 트리 데이터 구조

  - 근처 개체를 그룹화하고 트리의 다음 상위 수준에서 최소 경계 사각형 으로 개체를 표시

  참고 자료: [r_tree](https://en.wikipedia.org/wiki/R-tree) , [설명 블로그](https://jwkim96.tistory.com/298)

  </div>
</details>


  </div>
</details>

## 💡정규화에 대해 설명해주세요.

<details>
  <summary><b>정규화</b></summary>
  <div markdown="1">
하나의 릴레이션에 하나의 의미만 존재하도록 릴레이션을 분해하는 과정
- 데이터의 일관성, 최소한의 데이터 중복, 최대한의 데이터 유연성을 위한 방법 

### 제 1 정규형
테이블의 컬럼이 원자 값(Atomic Value; 하나의 값)을 갖도록 분해

### 제 2 정규형
제1 정규형을 만족하고, 기본키가 아닌 속성이 기본키에 완전 함수 종속이도록 분해

### 제 3 정규형
제2 정규형을 만족하고, 이행적 함수 종속을 없애도록 분해

### BCNF 정규형
제3 정규형을 만족하고, 함수 종속성 X → Y가 성립할 때 모든 결정자 X가 후보키가 되도록 분해

  </div>
</details>

## 💡정규화에는 어떤 장점이 있고 어떤 단점이 있는지 아는대로 설명해주세요.

<details>
  <summary><b>장단점</b></summary>
  <div markdown="1">

### 장점
- 데이터베이스 변경 시 이상현상이 발생하는 문제점을 해결 가능
- 데이터베이스 구조 확장 시 정규화된 데이터베이스는 그 구조를 변경하지 않아도 되거나 일부만 변경 가능

### 단점
- 릴레이션의 분해로 인해 릴레이션 간의 연산(JOIN 연산)이 많아짐. 이로인해 질의에 대한 응답 시간이 느려질 수 있음
- 속도가 느려질 수도, 빨라질 수도 있음(데이터 용량의 최소화)

  </div>
</details>

## 💡 역정규화를 하는 이유에 대해 아는대로 설명해주세요.

<details>
  <summary><b>역정규화</b></summary>
  <div markdown="1">

1. 성능 향상
- 성능 문제가 있는(읽기작업이 많이 필요한) DB의 전반적인 성능을 향상시키기 위함

2. 이유
- 정규화로 인해 성능이 저하될 수 있기 때문
- 정규화를 거치면 릴레이션 간의 연산(JOIN 연산)이 많아짐
  </div>
</details>


<br> <br> <br> <br> <br> <br>

# Reference

[기술 면접 정리](https://dev-coco.tistory.com/158)
# ⛓ RDBMS와 NoSQL


## 💡 RDB

> 관계형 데이터 모델에 기초를 둔 데이터베이스

- 대용량 데이터를 영구적으로 저장, 관리, 접근할 수 있음
- 테이블마다 스키마를 정의해야 함
- 데이터 타입과 제약(Constraint)를 통해서 데이터의 정확성을 보장
- **성능을 높이려면 더 좋은 하드웨어를 사용해야 함 (Scale Up)**

## 💡 RDBMS

> 관계형 데이터베이스(RDB)를 관리할 수 있는 소프트웨어

- MySQL, Oracle, MSSQL, PostgreSQL, MariaDB ...
- SQL 질의문을 통해 요청을 처리
- Oracle이나 Mysql 같은 제품은 'DBMS이며 데이터베이스가 아니다.'

## 💡 NoSQL

> Not only SQL, 대량의 비정형 데이터 저장&처리에 적합

- MongoDB, HBase, Redis ...
- 트랜잭션 기능(ACID)을 제공하지 않음
- **저렴한 비용으로 여러 대의 컴퓨터에 데이터를 분산,저장,처리하는 것이 가능 (Scale Out)**
- 데이터 구조를 미리 정의할 필요가 없음

## 💡 In-Memory DB

> NoSQL 방식에 속하는 데이터베이스, Key-Value 방식을 사용

- H2, Redis, Apache Derby Database(JavaDB), LMDB ...
- 메모리의 가격이 충분히 낮아지면서 빠른 데이터베이스 성능을 위해서 등장
- 디스크 대신 메모리를 사용해 I/O 성능이 좋음

# 💥 RDB VS NoSQL
> 두 방식 중 좋고 나쁨 없이 목적에 맞게 사용

| 구분        | RDB                                | NoSQL                             |
|----|------------------------------------|-----------------------------------|
| 처리 데이터    | 정형 데이터                             | 정형 데이터, 비정형 데이터                   |
| 대용량 데이터   | **❗대용량 처리 시 성능 저하❗**               | **✅대용량 데이터 처리에 적합**                    |
| 스키마       | 미리 정해진 스키마가 존재                     | 스키마가 없거나 변경이 자유로움                 |
| 트랜잭션      | 트랜잭션을 통해 **✅일관성 유지**를 보장함          | **❗트랜잭션을 지원하지 않아❗** 일관성 유지를 보장하기 어려움 |
| 검색 기능     | 조인 등의 **✅복잡한 검색 기능** 제공             | 단순한 데이터 검색 기능 제공                  |
| 확장성       | 클러스터 환경에 적합하지 않음                   | **✅클러스터 환경에 적합**                       |
| 라이선스      | (대부분)고가의 라이선스 비용                   | (대부분)오픈소스                         |
| 대표적 사례    | MySQL, PostgreSQL, Oracle, MariaDB | MongoDB, Redis, HBase             |

<br>

# ❓ 예상 질문

- NoSQL이 생겨난 이유와 특징에 대해 설명해 주세요
- RDB와 NoSQL을 비교해서 설명해주세요
- RDB의 장점, 단점을 설명해주세요
- NoSQL의 장점, 단점을 설명해주세요
- In-Memory DB가 무엇인가요?

<br>

# 👁‍🗨 Reference

- [RDBMS와 NoSQL](https://github.com/devSquad-study/2023-CS-Study/blob/main/DB/db_rdbms_and_nosql.md)
- [RDB, NoSQL, In-Memory DB 비교](https://toma0912.tistory.com/83)
- [RDB, RDBMS 란?](https://jwprogramming.tistory.com/52)
- [RDBMS vs NoSQL vs InMemory](https://pjt3591oo.github.io/blog/database/2017/04/06/about-database.html)

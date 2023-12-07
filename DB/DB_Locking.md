# 🔗 DB Locking


## 💡 Lock이 뭔가요?

> 트랜잭션 처리의 순차성을 보장하기 위한 방법

```
조용준 교수님의 개쩌는 겨울 계절학기 강의
수강신청 시스템에서 정원이 1명 남은 상황
김민섭과 이가경이 거의 동시에 수강신청을 누른다면...?
```

## 💡 Lock의 종류
### 공유(Shared) Lock
> 해당 데이터에 여러 세션이 Read 연산만 실행 가능 → Write를 막는 방식
- 데이터를 변경하지 않는 읽기 명령에 주어지는 락 (Shared Lock, S lock)
- 여러 세션에서 동시에 데이터를 읽어도 일관성에는 영향을 주지 않음
- 공유 락끼리는 동시에 데이터 접근 가능

### 배타(Exclusive) Lock
> 해당 데이터에 한 세션만 Read & Write 연산 모두 실행 가능 → 동시 접근을 막는 방식
- 데이터를 변경하는 쓰기 명령에 주어지는 락 (Write Lock, X Lock)
- 다른 세션이 해당 자원에 접근(SELECT, INSERT..) 하는 것을 막음
- 멀티 쓰레딩에서의 Mutex와 유사

## 💡 Lock의 설정 범위(Level)
```
한명이 수강신청 하는 동안 다른 사람들은...
1. 모든 과목 수강신청 금지 (데이터베이스 범위)
2. 해당 과의 모든 과목 수강신청 금지 (파일 범위)
3. 해당 과목만 수강신청 금지 (테이블 범위)
4. 해당 과목의 해당 자리 하나만 수강신청 금지 (행 범위)
```
- 데이터베이스 > 파일 > 테이블 > 페이지&블럭 > 열(column) / 행(row)
- 범위가 클 수록 제어가 간단하지만 병행 작업이 어려움
- 범위가 작을 수록 많은 수의 트랜젝션을 병행 수행 가능하지만 제어가 어려움
- 시스템에 따라 적절한 단위를 선택하는 것이 중요 (일반적으로 행 수준)
- 데이터베이스 단위 사용예시
    - DB의 소프트웨어 버전 업
    - 주요한 DB 업데이트
- 테이블 단위 사용예시
    - DDL(CREATE, ALTER, DROP...) 구문과 함께 사용됨
    - DDL Lock 이라고도 함
- 컬럼 단위의 경우 Lock 설정&해제의 리소스가 많이 들고 지원하지 않는 DBMS도 많아 일반적으로 사용하지 않음

## 💡 Blocking
> Lock의 경합(서로 경쟁)이 발생하여 특정 세션이 정지된 상태

- [[S Lock](#공유shared-lock) + [X Lock](#배타exclusive-lock)] 또는 [[X Lock](#배타exclusive-lock) + [X Lock](#배타exclusive-lock)]에서 발생
- 이전의 트랜잭션이 Transaction commit(종료) 또는 Rollback 을 하면 해결됨
- 성능에 좋지 않은 영향

    ### Blocking을 막으려면...?

  - **SQL 문장이 빠르게 실행되도록 리팩토링 (속도 개선)**
  - 트랜젝션을 가능한 짧게 정의 (허용 시간 단축)
  - 동일한 데이터를 동시에 변경하지 않게 설계
  - 작업 단위를 쪼개거나 Lock의 timeout을 설정

  ### 비관적 락(Pessimistic lock)
    - 동시성 문제가 발생할 것이라고 예상하고 lock을 걸어버리는 방법
    - 트랜잭션이 시작될 때 [S Lock](#공유shared-lock) 또는 [X Lock](#배타exclusive-lock)을 걸고 시작
    - 충돌이 자주 발생하는 환경에서 롤백의 횟수를 줄일 수 있으므로 성능에서 유리함
  
  ### 비관적 락(Pessimistic lock)
    - 동시성 문제가 발생하면 그때 가서 처리하는 방법
    - 충돌이 안난다는 가정하에, 동시 요청에 대해서 처리 성능이 좋음
    - 잦은 충돌이 일어나는 경우, 롤백 처리에 대한 비용이 큼

## 💡 DeadLock(교착 상태)
> 두 개 이상의 트랜잭션이 서로가 독점한 데이터의 unlock을 대기하는 상태

### DeadLock의  발생 조건
> 상호배제, 점유대기, 비선점, 순환대기 4 가지 조건이 동시에 성립할 때 일어남

1. 상호 배제(Mutual Exclusion)
   - 자원은 한 번에 한 프로세스만이 사용할 수 있어야 함
2. 점유 대기(Hold & Wait)
   - 자원을 점유하고 있으면서 다른 프로세스에 할당되어 사용하고 있는 자원을 추가로 점유하기 위해 대기하는 프로세스가 있어야 함
3. 비선점(No Preemption)
    - 다른 프로세스에 할당된 자원은 사용이 끝날 때까지 강제로 빼앗을 수 없어야 함
4. 순환 대기(Circular Wait)
    - 프로세스의 집합 {P_0, P_1, ... P_N-1}의 P_K가 P_(K+1)%N의 점유 자원을 대기하는 형태

### DeadLock의 해결 방법
> 예방(prevention), 회피(Avoidance), 탐지 후 회복(Detection & Recovery)

1. 예방(prevention)
    - [DeadLock의 발생 조건](#deadlock의--발생-조건) 중 하나를 제거하면서 해결
    - 자원 낭비가 심함
2. 회피(Avoidance)
    - DeadLock 발생 가능성을 인정하면서도 적절하게 회피
    - 다익스트라의 은행원 알고리즘
      - 은행에서 모든 고객의 요구가 충족되도록 현금을 할당하는데서 유래함
      - 프로세스가 자원을 요구할 때, 시스템은 자원을 할당한 후에도 안정 상태로 남아있게 되는지 사전에 검사하여 교착 상태 회피
      - 안정 상태면 자원 할당, 아니면 다른 프로세스들이 자원 해지까지 대기
3. 탐지 후 회복(Detection & Recovery)
    - 시스템에 DeadLock이 발생했는지 여부를 탐지(Allocation, Request, Available 등)
    - DeadLock을 일으킨 프로세스를 종료하거나, 할당된 자원을 해제

<br>

# ❓ 예상 질문

- Lock의 종류 2가지에 대해 설명해주세요
- Blocking과 그 해결 방안에 대해 설명해주세요
- DeadLock에 대해서 설명해주세요

<br>

# 👁‍🗨 Reference

- [DB Locking](https://github.com/devSquad-study/2023-CS-Study/blob/main/DB/db_locking.md)
- [[데이터베이스] Lock에 대해서 알아보자 - 기본편](https://sabarada.tistory.com/121)
- [데드락 (DeadLock, 교착 상태)](https://gyoogle.dev/blog/computer-science/operating-system/DeadLock.html) 
- [[운영체제] 데드락(Deadlock, 교착 상태)이란?](https://chanhuiseok.github.io/posts/cs-2/)

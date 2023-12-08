# 동기와 비동기

## Block
> 다른 함수가 실행을 시작하면 제어권이 넘어감
- 사장에게 보고서 제출 -> 사장이 다 읽을 때까지 대기 -> 사장 컨펌 후 자신의 자리로 복귀

## Non-Block
> 다른 함수가 실행을 시작해도 제어권을 다시 받음
- 사장에게 보고서 제출 -> 자신의 자리로 복귀해서 다른 업무 진행

## Block vs Non-Block
> 제어의 관점

---

## 동기란?
> 다른 함수의 실행 결과를 받음과 동시에 처리 시작
- 보고서 반려당함 -> 바로 수정사항에 대해 보고서 재작성

## 비동기란?
> 다른 함수의 실행 결과를 받아도 자신의 작업이 끝나면 처리 시작
- 보고서 반려당함 -> 일단 옆에 쌓아놓고 내가 하던 업무 처리 후 하고 싶을 때 들춰봄

## 동기 VS 비동기
> 순서와 결과(처리)의 관점

---
## 콜백 함수
> 다른 함수의 매개변수로 넘겨준 함수
- 콜백 지옥 : 콜백함수를 익명함수로 전달하다 보면 함수 호출이 너무 많이 반복되서 들여쓰기가 보기 힘들 정도로 깊어지는 현상

## Promise
> 자바스크립트 비동기 처리에 사용되는 객체
- 자바스크립트는 비동기 처리를 하는데 서버에 요청한 데이터를 다 받아오지도 않았는데 화면에 표시를 하려면 에러나 빈화면 출력 <br/>-> 그래서 이 요청 처리해 줄것이라 약속(promise)가 필요!

### promise 기본 문법 형식

  ![promise 기본 문법](./images/promise-basic.png)

### promise 상태

  ![promise 상태](./images/promise-state.png)

## aysnc / await
> 비동기 코드를 동기적으로 수행하는 프로미스 코드를 좀 더 깔끔하게 사용하기 위해 사용

### 프로미스 체이닝 방지
<p align="center" width="100%">
    <img src="./images/promise-chaining.png" width="49%">
    <img src="./images/async-await-wow.png" width="49%">
</p>

- async : "이건 비동기야"
  - 비동기 처리를 하고 싶은 함수 앞에 선언
- await : "기다려!"
  - async 함수 안에서만 사용 가능
  - await가 앞에 붙은 비동기 함수는 동기적으로 작동

### 그럼 이거 항상 쓰면 되나?
- 콜백 깊이가 깊지 않을 때는 굳이 사용할 필요 없음
- async/await으로 해결할 수 없는 동작을 Promise로 해결할 때도 있음

## JS는 싱글 스레드인데 어떻게 비동기 처리를 하지?

### 싱글 스레드
> 쉽게 말해 하나의 콜 스택에 처리해야할 함수 하나씩 넣어놓고 꺼내서 하나씩 처리한다는 것

![webapi-example](./images/webapi.png)

- setTimeout 등과 같은 함수들은 WebAPI이다<br />-> 브라우저가 대신 처리하다가 완료하면 task queue에 콜백 함수를 넣는다
<br>-> JS는 콜 스택이 빌 때까지 기다리다가 전부 비워지면 task queue를 살펴본다.<br>-> task queue에서 하나씩 빼서 콜 스택에 올려 처리한다.

- 그렇기에 setTimeout의 delay는 콜백함수의 딜레이 최소시간을 보장하지 정확한 딜레이 시간을 보장하지는 않는다.

# 예상 질문
- 동기와 비동기를 비교해서 설명해 주세요.
- Block과 Non-Block 방식에 대해 비교해서 설명해주세요.

# 레퍼런스
- [동기식 (Synchronous) / 비동기식 (Asynchronous) 이란?](https://tlsdnjs12.tistory.com/12)
- [어쨌든 이벤트 루프는 무엇입니까? | Philip Roberts | JSConf EU](https://www.youtube.com/watch?v=8aGhZQkoFbQ&t=1226s)
- [[10분 테코톡] 🐰 멍토의 Blocking vs Non-Blocking, Sync vs Async](https://www.youtube.com/watch?v=oEIoqGd-Sns)
- [[10분 테코톡] 🎧 우의 Block vs Non-Block & Sync vs Async](https://www.youtube.com/watch?v=IdpkfygWIMk)

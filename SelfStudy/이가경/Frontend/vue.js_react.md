> :bulb: 라이브러리와 프레임워크 차이 : 제어 흐름의 주도권이 누구에게 있느냐 <br>
> `라이브러리` : 전체적인 흐름을 개발자가 구현, 라이브러리를 가져다 써서 흐름을 구현 <br>
> `프레임워크` : 전체적인 흐름 제어, 개발자는 그 흐름 안에서 구현

# 📗 Vue.js
> `프레임워크`
- <b>프로그레시브 프레임워크</b> : 통상적인 프레임워크보다 자유도가 높음
  - 라이브러리처럼 사용될 수 있도록 설계
- 프레임워크이기 때문에 `.vue` 파일 형태에 맞춰 개발
  - `.js`로도 가능하지만 효율성이 떨어짐
- [SPA](/Frontend/frontend_spa_and_mpa.md/#spa란)
- [SSR](/Frontend/frontend_spa_and_mpa.md/#ssrserver-side-rendering)

## :memo: .vue
- 싱글 파일 컴포넌트(`SFC` : Single-File Component)
- 논리(Javascript), 템플릿(HTML), 스타일(CSS)을 하나의 파일에 캡슐화

<br>

```vue
<script>
export default {
  data() {
    return {
      count: 0
    }
  }
}
</script>

<template>
  <button @click="count++">숫자 세기: {{ count }}</button>
</template>

<style scoped>
button {
  font-weight: bold;
}
</style>

```

<br>

# 📘 React
> `UI 라이브러리`
- 라이브러리이기 때문에, 참조가 쉽고 라이브러리의 일부 기능만 가져와서 사용 용이
- 리액트 자체만으로는 상태관리, 라우팅 등을 지원하지 않기 때문에 redux, mobx 등을 사용해야 함
  - 상태관리 트렌드나 미들웨어에 대한 이해도 필요 -> 높은 러닝커브


<br>

# 🔎 유사성
- [Virtual DOM](#virtual-dom)
- 컴포넌트 기반

## 📚 Virtual Dom
> :bulb: [DOM](/Frontend/browserStruct.md/#dom에-대해서-간단히-알아보자) : HTML이나 XML 문서를 프로그래밍 언어에서 사용할 수 있도록 트리 구조로 구성해놓은 것   
>
> javascript로 DOM을 조작하게 된다면, 각각의 변경사항마다 하나씩 해석하여 재렌더링 -> <b>높은 렌더링 비용!!</b> -> 하나의 element를 갱신하는 것보다 <b>더 큰 부분을 갱신</b>하는게 훨씬 <b>적은 비용</b> 소모

- 실제 DOM의 copy 개념
- DOM의 구조를 javascript 객체로 표현
- 모든 변경은 Virtual DOM에 반영이 된 후, **실제 DOM과 Virtual DOM을 비교해 <u>달라진 부분만</u> 변경**
  - 달라진 부분은 `diffs`에 저장

  `변경 내역들`
  ```javascript
  const diffs = [
    {
      newNode: {},
      oldNode: {},
      index:
    },
    {
      newNode: {},
      index: {}
    }
  ]
  ```
  <br>

  `변경 과정`
  ```javascript
  const domElement = document.getElementsByClassName("list")[0];

  diffs.forEach((diff) => {
    const newElement = document.createElement(diff.newNode.tagName);

    if(diff.oldNode) {
      // old version이 있다면 replace
      domElement.replaceChild(diff.newNode, diff.index);
    } else {
      // 아니라면 new node 생성
      domElement.appendChild(diff.newNode);
    }
  })
  ```

  ### 🏃 동작 원리
  1. UI가 변경되면 전체 UI를 Virtual DOM으로 렌더링
  2. 현재 Virtual DOM과 이전 Virtual DOM을 비교해 차이를 계산
  3. 변경된 부분만 실제 DOM에 반영

<br>

# 🔎 차이점

> :crown: <b>Winner</b> <br>
> 사용성과 생산성 측면 : `Vue.js` <br>
> 트렌드나 범용성 측면 : `React` 


## 🗽 자유도
> :crown: <b>Winner</b> <br>
> `React`

- 조건에 따라 버튼이 보이게 구현하는 방식 예시

`React` 
```
// && 연산자 방식
<div>
   {isVisible && <button> 조건에 따라서 사라지는 버튼 </button>}
</div>

// 삼항연산자 방식
<div>
   {isVisible ? <button>조건에 따라 사라질 버튼</button> : null}
</div>
```

`Vue.js`
```
<div>
   <button v-if="isVisible">조건에 따라서 사라질 버튼</button>
</div>
```

<br>

=> `React`의 경우 `&& 연산자` 혹은 `삼항연산자`로 구현 가능하지만, `Vue.js`의 경우 `v-if` 만 사용 가능

## ♻ 재사용성
> :crown: <b>Winner</b> <br>
> `React`

- 컴포넌트 분리에 있어서 `React`는 한개의 파일 내에서 새로운 함수를 통해 생성 가능
- `Vue.js`는 컴포넌트 분리하기 위해 새로운 파일 생성 필요
  - 상황에 따라 `<template>`, `<style>`, `<script>` 작성 필요

<br>

## 🛣 상태 갱신 성능
> :crown: <b>Winner</b> <br>
> `Vue.js`

- `React`는 상태 변경 시, 해당 컴포넌트부터 자식 컴포넌트까지 재렌더링 (개발자가 최적화 가능)
-  `Vue.js`는 렌더링 중 컴포넌트 종속성이 <b>자동 추적</b>되어 시스템은 실제로 <b>재렌더링 대상이 누군지 알고 있음</b>

=> `React`를 최적화 하더라도, `Vue.js`가 더 빠름

<br>

# :question: 예상 질문

<details>
<summary>
프로젝트에서 리액트를 사용한 이유는 무엇인가요? </summary>
<div markdown="1">
Vue.js와 React를 사용해본 경험이 있는데, <b>높은 자유도와 재사용성</b>으로 인해 Vue.js가 아닌 React를 선택했습니다.

<br>
Vue는 프레임워크이고 React는 라이브러리인데, Vue는 프레임워크 특성 상 짜여진 틀 안에 구현해야해서 React에 비해 자유도가 낮다고 생각해서 React를 선택했습니다. <br> <br>
또한 Vue의 경우 컴포넌트를 분리하기 위해선 새로운 파일을 생성해야하는데, React는 한개의 파일 안에서 새로운 함수를 통해 컴포넌트를 분리할 수 있어 재사용성이 높아 선택했습니다.

</div>
</details>

<br>

<details>
<summary>
Virtual DOM에 대해 아는대로 설명해주세요. </summary>
<div markdown="1">
DOM의 구조를 javascript 객체로 표현한 것으로, 높은 렌더링 비용이 드는 DOM을 보완할 방법으로 나타나게 되었습니다.
<br>
DOM의 경우, 여러 변경사항이 존재하게 되면 각각의 변경사항마다 하나씩 해석해서 재렌더링을 하게 되어 높은 렌더링 비용이 듭니다.
<br>
그러나 Virtual DOM을 사용할 경우 Virtual DOM에서 변경된 부분만 DOM에 적용하여 효율적으로 렌더링이 가능해집니다.
<br>
예를 들자면, 방의 가구 위치를 변경하고자 할 때, 
<br>
DOM의 경우 가구를 직접 옮기는 것이지만 <br>
Virtual DOM의 경우 설계도에서 가구 위치를 조정하고, 이후 실제 가구 위치를 변경하는 것이라고 할 수 있습니다.


</div>
</details> 

<br>

# :newspaper: Reference

- [v3 docs: vue.js 소개](https://v3-docs.vuejs-korea.org/guide/introduction.html)
- [리액트와 뷰의 차이](https://brunch.co.kr/@skykamja24/573)
- [같은 앱 구현을 통한 리액트와 뷰의 차이점 알아보기](https://erwinousy.medium.com/%EB%82%9C-react%EC%99%80-vue%EC%97%90%EC%84%9C-%EC%99%84%EC%A0%84%ED%9E%88-%EA%B0%99%EC%9D%80-%EC%95%B1%EC%9D%84-%EB%A7%8C%EB%93%A4%EC%97%88%EB%8B%A4-%EC%9D%B4%EA%B2%83%EC%9D%80-%EA%B7%B8-%EC%B0%A8%EC%9D%B4%EC%A0%90%EC%9D%B4%EB%8B%A4-5cffcbfe287f)
- [React, Vue와 비교하기](https://velog.io/@jjunyjjuny/React-vs-Vue)
- [Virtual DOM에 대해](https://medium.com/sjk5766/virtual-dom%EC%97%90-%EB%8C%80%ED%95%B4-7222d752ee65)
- [Virtual DOM 동작 원리 및 Vue.js에서의 Virtual DOM](https://tech.osci.kr/%EC%9E%91%EA%B3%A0-%EC%86%8C%EC%A4%91%ED%95%9C-vue%EC%97%90-%EB%8C%80%ED%95%B4-%EC%95%8C%EC%95%84%EB%B3%B4%EC%9E%90%EA%B0%9C%EC%9A%94/)

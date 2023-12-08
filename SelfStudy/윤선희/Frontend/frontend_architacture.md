# 프론트엔드 아키텍처

## 프론트엔드 트렌드 변천사

[![](./images/frontend_img01.png?width=400px)]()
<br><br>

## 프론트엔드 아키텍처 변화

### MVC ➡️ MVVM ➡️ MVI

<br>

### 🎨 MVC 아키택처

> Model + View + Controller  

[![](./images/frontend_img02.png?width=400px)]()

- **Model**: 화면에 보여줄 데이터를 담당하는 영역. Model의 정의는 주어진 환경에 따라서 다를수 있다. (Javascript의 Object, 서버의 DB, 서버에서 API로 요청한 데이터 등)
- **View**: 실제 사용자에게 보여지는 화면 (HTML + CSS 로 만들어지는 결과물)
- **Controller**: Model의 데이터를 받아서 화면에 그리고, 화면으로부터 사용자의 동작을 받아서 Model을 변경, **Model과 View사이의 중간 역할을 하는 것**

#### ❓MVC 로 레이어를 나눈 이유❓

1. 화면을 다루는 문제와 데이터를 다루는 문제의 성격이 달라서
2. Model과 View 간의 의존 관계를 최소화 해서 각자의 수정이 서로에게 영향을 미치지 않게 하기 위해

<br><br>

### 🎨 MVVM 아키텍처

> Model + View + View Model

#### 등장배경

jQuery로 작업을 하다보니 데이터를 수정하고 이벤트를 연결하고 수정하는 과정이 계속 반복된다는 불편한 점이 생김. 이러한 불편함을 해소하기 위해 Angular가 등장.  
앵귤러에서는 템플릿과 바인딩이라하는 중요한 개념들이 등장하였고 이후로 웹 개발하는 방식의 패러다임이 바뀜.

- **View Model**: 코드에서 DOM을 조작하는 코드가 사라지고 이 기능들은 프레임워크가 담당하게 된다. 개발자는 화면에 그려져야할 `데이터만 만들어서` 프레임워크에 `전달`해주면 프레임워크가 알아서 그려줌. 이것을 View를 그리는 Model만 다루게 되었다는 의미로 **ViewModel**이라고 부름.
  <br>

이후 등장한 React, Vue, Angular2, Svelte등 어떤 방식의 템플릿과 바인딩 문법을 쓰느냐 방식만 다를뿐 MVVM 아키텍처는 그대로 유지된다.  

<br>

### ✨ MVC 와 MVVM의 차이점(달라진 점)

- 컨트롤러의 반복적인 기능이 `선언적인 방식`으로 개선
- Model과 View의 관점을 분리하려 하지 않고 `하나의 템플릿`으로 관리하려는 방식을 발전(기존에는 class나 id등으로 간접적으로 HTML에 접근하려고 했다면 이제는 직접적으로 HTML에 접근하는 방법으로 확장)  

<br><br>

### 🎨 Componet 패턴과 Container-Presenter 패턴
#### 🎗 Componet 패턴
- 재사용이 가능한 작은 단위로 만들어서 조립하여 화면을 구성할 수 있는 패턴
- 컴포넌트는 재사용이 가능해야한다는 원칙을 따르기 위해선 비즈니스 로직이 포함되지 않도록 해야한다.  

#### 🎗 Container-Presenter 패턴
- Container 컴포넌트 : 비즈니스 로직을 관장하는 컴포넌트
- Presenter 컴포넌트 : 비즈니스 로직이 없는 데이터만 뿌려주는 형태의 컴포넌트

<br>

최상단이나 1depth에 Container를 두고 비즈니스 로직을 관리하는 것이 `Container-Presenter 패턴` 이다.<br>
그러나 이것 또한 `React Hook` 의 등장으로 용도의 중요성이 떨어졌다. (⬅ 클래스형 컴포넌트를 만들때의 이야기임)  

<br>

### 💥 Props Drilling Problem  💥
컴포넌트의 구조가 복잡해짐에 따라 하위에 특정 값을 전달하기 위해 중간 레벨에 있는 컴포넌트들은 필요가 없음에도 전달하기 위해 그 props을 가지고 있어야하는 문제점이 발생함. (컴포넌트의 재사용과 독립성을 지나치게 강조하다보니 발생한 문제)
<br>
[![](./images/frontend_img03.png?width=400px)]()
<br>

이러한 Props Drilling Problem 을 해결하기 위해 새로운 아키텍쳐가 등장하는데.... <br>
그게 바로 `FLUX 패턴` 과 `Redux` 이다.

<br><br>

### 🎨 FLUX 패턴
[![](./images/frontend_img04.png?width=400px)]() <br>

> MVC 패턴에서 벗어나 단방향 아키텍처(uni-directional architecture)를 만들자고 해서 나온 패턴
> View를 하나의 범주로 두고 View에서 Action을 호출하면 Dispatcher를 통해 Store라는 공간에 Data가 보관이 되고 이것을 다시 View로 전달되는 흐름

### 🎨 Redux
FLUX 패턴을 활용한 구현체가 바로 Redux이다. <br>
기존의 Props Drilling Problem을 정확히 집어주면서 Store, Dispatch, Reducer에 대한 개념을 정확하게 다시 정리해주었다. <br>

[![](./images/frontend_img05.gif?width=400px)]() <br>

> View를 MVC 컴포넌트 관점으로 보는 것이 아니라 하나의 큰 View로 이해하고,  <br>
> View는 Dispatcher를 통해 Action을 전달하면,  <br>
> Action은 Reducer를 통해서 Data가 Store에 보관이 되고,   <br>
> Store에 들어있는 데이터는 다시 View로 연결이 되는 방식

<br>

즉, 기존의 컴포넌트 단위의 MVC 개념에서 비즈니스 로직과 View를 완전히 분리된 개념을 **상태관리(State Management)** 라고 한다.

<br>

#### ✨ MVC에서 FLUX으로 오면서 달라진 점
- 공통적으로 사용되는 비지니스 로직과 View를 완전히 분리되어 **상태관리**라는 방식으로 관리한다.
- 각각의 독립된 컴포넌트가 아니라 `하나의 거대한 View 영역`으로 간주한다.
- 둘 사이의 관계는 `Action과 Reduce라는 인터페이스로 분리`하며 Controller는 이제 양방향이 아니라 `단반향`으로 Cycle을 이루도록 설계한다.

<br>

### FLUX 패턴의 한계
> 🛑 긴 러닝커브  <br> 
> 🛑 장황한 문법

<br>

상태를 관리하기 위해 부수적인 코드들이 많이 사용되어 오히려 관리가 어려워진 것 같다는 문제점 발생.

<br><br>

### 🎨 MVI 패턴  
<br>

[![](./images/frontend_img06.png?width=400px)]() <br>

웹프론트에서는 cycle.js 라는 라이브러리에서 먼저 나왔던 개념이다.  <br>
기존 FLUX 패턴을 Dispatch와 Action과 Update의 인터페이스를 전부 **Observable를 이용한 스트림(Stream)** 의 하나의 방식으로 만들어 비동기 문제를 해결하고 장황한 문법을 **하나의 인터페이스**로 만든 점이 인상적인 아키텍쳐. <br>

✨ **MVI 아키텍처는 현재 웹보다는 android 와 ios 같은 모바일에서 주로 활용되고 있는 아키텍처라고 한다.** ✨ <br>

> Model + View + Intent

<br>

> **Model** : Model 은 상태를 나타낼 수 있다. MVI에서 Model은 데이터의 플로우가 `단방향`으로 이루어지기 위해 무조건 `불변성`을 보장해야 한다. <br>
> **View**: View는 Activity나 Fragment를 나타내며, 상태를 전달 받아 화면에 랜더링하는 역할이다. <br>
> **Intent**: 사용자가 작업을 수행하려는 `의도(intent)`를 나타냅니다. 모든 사용자 작업에 대해 View로부터 의도(intent)를 수신하고 Presenter에서 이를 관찰하고 Model에서 새로운 상태로 변환합니다.

<br><br>

## 현대 웹프론트엔드 아키텍처의 방향성

### Context와 hook, props 상속
FLUX 패턴과 같은 복잡한 문법을 가지고 만드는 Redux보다는 **Hook**과 같은 Context API를 활용하고자하는 움직임.  
View와 Model을 분리하고 Props Drilling Problem을 막는 것에 집중하자는 의도.

<br>

### 🎨 Atomic 패턴 
<br>

[![](./images/frontend_img07.png?width=400px)]() <br>

> Recoil, Svelte Store, Vue Composition, jotai 등

<br>

- 상태관리에는 동의하나 복잡한 구조를 가져야하나에 대해 회의적인 시각으로 나온 패턴
- 간단한 문법으로 컴포넌트 외부에서 공통의 데이터를 set, get할 수 있게 하면서 동시에 동기화할 수 있는 것
- 중간의 과정은 자율에 맡기고 간단하게 Model에 접근하는 법만 제공하자.
- 동기화, 동시성 처리가 중요

<br><br>

### 🎨 React-Query

최근에 우아한 형제들과 카카오 계열사 일부에서 사용한다는 React-Query이다.

> - MVC의 개념 확대로 상태관리에 편향되어 있던 시각에서 벗어나 고전적인 ajax의 데이터를 Model로 간주한다.
> - 서버와의 fetch영역을 Model로 간주
> - View가 React
> - Controller는 query와 mutation이라는 2가지의 인터페이스를 통해서 서버 데이터의 상태를 관리하고 캐싱, 동기화, refetch등을 관리해주는 역할
> - 가장 큰 사용이유 : 클라이언트 데이터의 상태관리와 서버 데이터의 상태관리를 나누어 사용해, 유지보수의 편의성을 높인다.


<br><br>

# :question: 예상 질문

<details>
  <summary><b>MVVM 패턴에 대해서 설명해주세요.</b></summary>
  <div markdown="1">
  </div>
</details>
<br>

<details>
  <summary><b>Props Drilling Problem 에 대해서 설명해주시고 어떤 해결방법이 있는지 아시는대로 얘기해주세요.</b></summary>
  <div markdown="1">
  
  </div>
</details>
<br>

<details>
  <summary><b>상태관리를 해보신 경험이 있다면 혹시 사용해본 라이브러리에 대해서 설명해주실 수 있을까요?</b></summary>
  <div markdown="1">
  
  </div>
</details>
<br>

    

# :newspaper: Reference
[프론트엔드 트렌드](https://yozm.wishket.com/magazine/detail/1663/)
[프론트엔드 아키텍처란? - 테오블로그](https://velog.io/@teo/%ED%94%84%EB%A1%A0%ED%8A%B8%EC%97%94%EB%93%9C%EC%97%90%EC%84%9C-MV-%EC%95%84%ED%82%A4%ED%85%8D%EC%B3%90%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80%EC%9A%94)

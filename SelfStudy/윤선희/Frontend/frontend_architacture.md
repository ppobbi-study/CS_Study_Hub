# 프론트엔드 아키텍처

## 프론트엔드 트렌드 변천사

[![](./images/frontend_img01.png?width=400px)]()
<br><br>

## 프론트엔드 아키텍처 변화

### MVC ➡️ MVP ➡️ MVVM ➡️ MVI

<br>

### MVC 아키택처

> Model + View + Controller

- **Model**: 화면에 보여줄 데이터를 담당하는 영역. Model의 정의는 주어진 환경에 따라서 다를수 있다. (Javascript의 Object, 서버의 DB, 서버에서 API로 요청한 데이터 등)
- **View**: 실제 사용자에게 보여지는 화면 (HTML + CSS 로 만들어지는 결과물)
- **Controller**: Model의 데이터를 받아서 화면에 그리고, 화면으로부터 사용자의 동작을 받아서 Model을 변경, Model과 View사이의 중간 역할을 하는 것

#### ❓MVC 로 레이어를 나눈 이유❓

1. 화면을 다루는 문제와 데이터를 다루는 문제의 성격이 달라서
2. Model과 View 간의 의존 관계를 최소화 해서 각자의 수정이 서로에게 영향을 미치지 않게 하기 위해

### MVVM 아키텍처

> Model + View + View Model

#### 등장배경

jQuery로 작업을 하다보니 데이터를 수정하고 이벤트를 연결하고 수정하는 과정이 계속 반복된다는 불편한 점이 생김. 이러한 불편함을 해소하기 위해 Angular가 등장.  
앵귤러에서는 템플릿과 바인딩이라하는 중요한 개념들이 등장하였고 이후로 웹 개발하는 방식의 패러다임이 바뀜.

- **View Model**: 코드에서 DOM을 조작하는 코드가 사라지고 이 기능들은 프레임워크가 담당하게 된다. 개발자는 화면에 그려져야할 `데이터만 만들어서` 프레임워크에 `전달`해주면 프레임워크가 알아서 그려줌. 이것을 View를 그리는 Model만 다루게 되었다는 의미로 **ViewModel**이라고 부름.
  <br>

이후 등장한 프레임워크인 React, Vue, Angular2, Svelte등 어떤 방식의 템플릿과 바인딩 문법을 쓰느냐 방식만 다를뿐 MVVM 아키텍처는 그대로 유지된다.

### ✨ MVC 와 MVVM의 차이점(달라진 점)

- 컨트롤러의 반복적인 기능이 `선언적인 방식`으로 개선
- Model과 View의 관점을 분리하려 하지 않고 `하나의 템플릿`으로 관리하려는 방식을 발전(기존에는 class나 id등으로 간접적으로 HTML에 접근하려고 했다면 이제는 직접적으로 HTML에 접근하는 방법으로 확장)

# :question: 예상 질문

<details>
  <summary><b> </b></summary>
  <div markdown="1">
  </div>
</details>
<br>
    

# :newspaper: Reference
[프론트엔드 트렌드](https://yozm.wishket.com/magazine/detail/1663/)

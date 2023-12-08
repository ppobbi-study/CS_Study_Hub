# React Hook

## 함수형 컴포넌트(Functional Component)의 생명주기 👉 Hook

리액트에서 Hook은 함수형 컴포넌트에서 React State와 생명주기 기능을 연동할 수 있게 해주는 함수이다.  
Hook은 class안에서는 동작하지 않으며, class 없이 React를 사용할 수 있게 한다.

### Hook의 특징

- 클래스형과 함께 사용할 수도 있다.
- Hook이 기존의 React 컨셉을 대체하는 것이 아니다. 대신에, Hook은 props, state, context, refs, 그리고 lifecycle와 같은 React 개념에 좀 더 직관적인 API를 제공한다.

### Hook 도입 목적

- 기존의 라이프사이클 메서드 기반(wrapper hell)이 아닌, 로직 기반으로 나눌 수 있어서 컴포넌트를 `함수 단위로 잘게 쪼갤 수 있다`는 장점
- 라이프사이클 메서드에는 관련 없는 로직이 자주 섞여 들여가는데, 이로 인해 버그가 쉽게 발생하고 무결성이 깨질 수 있다.

### ✅ Hook 사용 규칙 두가지 ✅

#### 1️⃣ 최상위에서만 Hook을 호출해야 한다.

- ❌ 반복문, 조건문, 중첩된 함수 내에서 Hook을 실행하면 안된다. ❌
- 이 규칙을 따르면 컴포넌트가 렌더링될 때마다 항상 동일한 순서로 Hook이 호출 되는 것을 보장한다.

#### 2️⃣ 리액트 함수 컴포넌트에서만 Hook을 호출해야 한다.

- ❌ 일반 JS 함수에서는 Hook을 호출해서는 안된다. ❌

<br>
<br>

## Hook의 종류

### 1️⃣ useState

가장 기본적인 빌트인 Hook으로서, 함수형 컴포넌트에서도 가변적인 상태를 지니고 있을 수 있게 해준다. 함수형 컴포넌트에서 상태를 관리해야할 때 사용

<br>

```
import React, { useState } from 'react';

const Counter = () => {
  const [value, setValue] = useState(0);
  return (
    <div>
      <p>
        현재 카운터 값은 <b>{value}</b> 입니다.
      </p>
      <button onClick={() => setValue(value + 1)}>+1</button>
      <button onClick={() => setValue(value - 1)}>-1</button>
    </div>
  );
};
```

<br>

> const [value, setValue] = useState(0);
> 배열 비구조화 할당문법이다. 함수 파라미터로 0이라는 기본값을 넣어준 것 상태값이 바뀌면 컴포넌트는 리랜더링 된다. 기본 값은 어떤 값도 들어갈 수 있다.(객체가 들어갈 수도 있음)

<br>

#### ❓ 그렇다면 우리 프로젝트에서 왜 useState로 지갑주소를 셋팅할 수 없었을까? ❓

[![](../images/react_img02.png?width=400px)]()

**setState의 동작 원리**

1. state가 바뀌면 화면 전체가 자동으로 다시 그려진다. (리렌더링)
2. setState는 비동기로 작동한다. = state의 값은 setState가 호출되는 시점이 아닌, 해당 코드가 들어있는 함수가 모두 실행된 이후에 바뀐다.

💡 **왜???** 💡

> setState가 비동기가 아닌 동기로 작동하게 되면 변경될 때마다 바로바로 렌더링을 하기 때문에 비효율적이다.

```javascript
await s3.upload(params, async (err: any, data: any) => {
			if (err) {
				alert('시스템 에러, 관리자에게 문의하세요.');
				setIsLoading(false);
				console.log("err", err);
				return;
			} else {
				try{
					await axios.post("https://idog.store/blockchain/uploadIpfs", {
							img: data.Location,
							petName: petName,
							petSpecies: petSpecies,
							petBirth: petBirth,
							petGender: petGender,
						}).then(async (data) => {
							const nftCid = data.data.nftCid;
							const imageOrigin = "https://ipfs.io/ipfs/" + data.data.imageCid;
							console.log("nftCid", nftCid);
							const overrides = {
								gasPrice: ethers.parseUnits('9000', 'gwei')  // gasPrice 설정 (예: 100 gwei)
							};

							const walletAddress = myWalletAddress;
							console.log("walletAddress", walletAddress);
							if (data.status=== 200) {
								const tx = await mintDogTokenContract.mintDogProfile(
									walletAddress,
									`ipfs://${nftCid}`
								);

    ...

```

<br>

### 2️⃣ useEffect

리액트 컴포넌트가 렌더링 될 때마다 특정 작업을 수행하도록 설정할 수 있는 Hook.  
Mount, Update, Unmount 가 합쳐진 형태라고 생각해도 된다.
<br>
❗️만약 화면을 다 그리기 이전에 동기화 되어야 하는 경우에는,useLayoutEffect를 활용하여 컴포넌트 렌더링 - useLayoutEffect 실행 - 화면 업데이트 순으로 effect를 실행시킬 수 있다.

```
useEffect(() => {}); // 렌더링 결과가 실제 돔에 반영된 후마다 호출
```

#### 1) 마운트 될 때만 실행하고 싶은 경우

만약 useEffect 에서 설정한 함수가 컴포넌트가 화면에 `가장 처음 렌더링 될 때`만 실행되고 업데이트 할 경우에는 실행 할 필요가 없는 경우엔 함수의 두번째 파라미터에 빈 배열[]을 넣는다.

```
useEffect(() => {
    console.log('마운트 될 때만 실행됩니다.');
  }, []);
```

#### 2) 특정 값이 업데이트 될 때만 실행하고 싶을 때

useEffect 의 두번째 파라미터로 전달되는 배열 안에 검사하고 싶은 값을 넣어준다.

```
useEffect(() => {
    console.log(name);
  }, [name]);

```

#### useEffect 에서 return은 정리(clean up)를 위해 사용된다.

- 메모리 누수 방지를 위해 UI에서 컴포넌트를 제거하기 전에 수행
- 컴포넌트가 여러 번 렌더링 된다면 다음 effect가 수행되기 전에 이전 effect가 정리된다.

<br>

<!-- ### 3️⃣ useRef

javascript에서 특정 Dom을 선택하는 역할 ex) getElementById, querySelector
특정 DOM에 접근할 때 사용한다.
외부 라ㅣ브러리 사용할때 유용하다.
원하는 위치에 ref={} 의 형태로 작성하면 된다.
포커스를 잡으려면 nameInput.current.focus() 형태로 작성하면 된다.

```
const nameInput = useReft();

const onClick = () => {
    nameInput.current.focus();
}

return(
    <input ref={nameInput} />
    <button onClick={onClick}>클릭</button>
)

``` -->

# :question: 예상 질문

<details>
  <summary><b>state를 직접 변경하지 않고 setState를 사용하는 이유에 대해서 설명하세요.</b></summary>
  <div markdown="1">
  state는 불변성을 유지해야하기 때문입니다. 컴포넌트는 setState를 비교해서 업데이트가 필요한 경우에만 render함수를 호출하는데 state를 직접 수정하게 되면 리액트가 render함수를 호출하지 않아 상태 변경이 일어나도 렌더링이 일어나지 않을 수 있습니다.
  </div>
</details>
<br>

<details>
  <summary><b>리액트 Hooks의 장점은 무엇인가요?</b></summary>
  <div markdown="1">
  Hooks의 장점은 로직의 재사용이 가능하고 관리가 쉽다는 것입니다. 함수 안에서 다른 함수를 호출하는 것으로 새로운 hook을 만들어 볼 수 있습니다. 기존의 class component는 여러 단계의 상속으로 인해 전반적으로 복잡성과 오류 가능성을 증가시켰습니다. 하지만 function component에 hooks에 도입되면서 class component가 가지고 있는 기능을 모두 사용할 수 있음은 물론이고 기존 class component 복잡성, 재사용성의 단점들까지 해결됩니다.
  </div>
</details>
<br>

<details>
  <summary><b>useEffect 메소드로 componentWillUnmount 가 동작할 수 있는 방법에 대해서 설명하세요.</b></summary>
  <div markdown="1">
  useEffect 코드 내부에서 return하는 익명함수를 작성하는 방법으로 componentwillUnmount를 구현할 수 있습니다.
  </div>
</details>
<br>
    
# :newspaper: Reference

[]()

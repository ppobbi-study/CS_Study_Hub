# Use.Memo

렌더링 최적화 함수, `memo`.

- `memo`는 react가 제공해 주는 함수
- 컴포넌트가 렌더링 되려할 때, props와 props를 비교해 바뀌지 않으면 렌더링 X

## 사용법

```
const MyComponent = React.memo(function MyComponent(props) {
  // 컴포넌트의 구현
  return <div>{/* ... */}</div>;
});
```

# useMemo

메모이제이션된 값을 반환하는 React hook

- `메모이제이션 피보나치 함수` 같이 직전에 연산된 값이 있다면, 다시 연산하지 않음
- 의존성이 변경되었을 때에만 메모이제이션된 값을 다시 계산

## 사용법

```
const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);
```

- 첫번째 인자에는 값을 연산하고 반환하는 함수를 넣어준다.
- 두번째 인자에는 의존성 배열을 넣어준다. (특정 값 a, b가 변경되었을 때 다시 연산하라고 알려주는 배열)

# UseCallback

- UseCallback 메모이제이션된 콜백 함수, 즉 이미 생성된 함수를 반환하는 React hook

## 사용법

```
const memoizedCallback = useCallback(
  () => {
    // 로직 작성
    doSomething(a, b);
  },
  // 의존성 배열
  [a, b],
);
```

- 콜백 함수: 첫 번째 인자로 전달되는 함수는 메모이제이션됨. 이 함수는 컴포넌트 내에서 필요한 로직을 수행.

- 의존성 배열: 두 번째 인자인 배열은 해당 함수가 의존하는 변수들을 포함. 이 배열에 포함된 변수 중 하나라도 변경되면, 함수가 재생성. 배열이 비어 있으면, 함수는 컴포넌트가 처음 렌더링될 때만 생성되고 이후에는 재생성되지 않음.

# 출처

- https://velog.io/@khy226/useMemo%EC%99%80-useCallback-%ED%9B%91%EC%96%B4%EB%B3%B4%EA%B8%B0

- https://www.nextree.io/riaegteu-rendeoring-mic-coejeoghwa/

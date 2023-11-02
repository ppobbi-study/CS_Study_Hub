# SPA와 MPA

## MPA란?
> Multi-Page Application, 전통적인 방식으로 사용자의 요청 시 각각의 페이지가 독립적으로 렌더링되는 웹 어플리케이션이나 웹사이트

### SSR(Server Side Rendering)
> 서버로부터 전체 html파일을 받아와서 페이지 전체를 렌더링
- 화면이 깜빡인 후 새로고침되어 표시됨

### 장점
- SEO(검색 엔진 최적화)에 유리
- 빠른 초기 로딩 속도

### 단점
- 매번 새로고침되므로 불편한 사용자 경험
- 페이지의 모든 리소스를 서버가 넘겨주므로 서버 부담 증가

---

## MPA to SPA
- 보여줘야 할 화면의 데이터가 많아짐에 따라 서버에 부담이 가중됨
- AJAX라는 비동기 통신 기술이 나옴에 따라 페이지의 새로고침 없이 내용 갱신이 가능해짐 -> SPA

## SPA란?
> Single-Page Application, 사용자의 요청 시 새로운 페이지를 불러오지 않고 단일 페이지 내에서 동적으로 다시 작성하는 웹 어플리케이션이나 웹사이트

### CSR(Client Side Rendering)
> 사용자의 요청에 따라 필요한 부분만 응답받아 렌더링

### 장점
- 빠른 속도 및 서버 부하 감소
- 사용자 친화적

### 단점
- SEO(검색 엔진 최적화)에 불리
- 모든 JS파일을 가져와야 되서 느린 초기 로딩 속도

## 그럼 무엇을 써야 하나?
- SPA가 SSR방식을 사용 못하는 것은 아님
- 단순 정보 제공에는 SSR, 동적 변화가 필요한 부분은 CSR로 구성

# 예상 질문
- SPA와 MPA에 대해 설명해주세요
- SPA와 MPA를 비교해주세요

# 레퍼런스
- [[10분 테코톡] 🍻주모의 SPA](https://www.youtube.com/watch?v=vM_zQLnlyKw)
- [[10분 테코톡] 🎨 신세한탄의 CSR&SSR](https://www.youtube.com/watch?v=YuqB8D6eCKE)
- [Are SPAs better than MPAs? | HTTP 203](https://www.youtube.com/watch?v=ivLhf3hq7eM)
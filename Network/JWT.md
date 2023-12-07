# JWT (Json Web Token)

> 인증에 필요한 정보들을 암호화시킨 JSON 토큰

- JSON 데이터를 `Base64 URL-safe Encode`를 통해 인코딩하여 직렬화 한 것

> `Base64 URL-safe Encode` : URL에서 오류없이 사용하도록 `+`, `/`를 각각 `-`, `_` 로 표현한 것

## JWT 구조

![jwt_const](./images/jwt_const.png)

### Header

- 토큰을 어떻게 검증하는가에 대한 내용
- alg : 서명 암호화 알고리즘
- typ : 토큰 유형

### Payload

> [`Claim`](#claim) : Key - Value 형식으로 이뤄진 한 쌍의 정보

- 토큰에서 사용할 정보 조각들인 `Claim`이 담겨 있음
- 누가 누구에게 발급
- 유효기간
- 토큰을 통해 공개하기를 원하는 내용
  - ex) 닉네임, 레벨, 관리자 여부 등
  - 서버가 데이터베이스에서 찾는 비용 감소

### Signature

- 부호화 시킨 header, payload + 서버가 지정한 secret key로 암호화시켜 토큰을 변조하기 어렵게 함
- 암호화 시, 헤더에서 정의한 알고리즘 방식(alg) 활용

### Claim

- Registed Claims : 미리 정의된 Claim
  - `iss` : issuer, 발행자
  - `exp` : expiration time, 만료 시간
  - `sub` : subject, 제목
  - `iat` : issued At, 발행 시간
  - `jti` : JWT ID
- Public Claims : 사용자가 정의한 Claim, 공개용 정보 전달을 위해 사용
- Private Claims : 해당하는 당사자 간에 정보 공유를 위해 만들어진 사용자 지정 Claim

## JWT 인증 과정

<br>

# :question: 예상 질문

<details>
<summary>
JWT에 대해 아는대로 설명해보세요</summary>
<div markdown="1">
<br>
인증에 필요한 정보들을 암호화시킨 JSON 토큰으로 header, payload, signature 세 부분으로 나뉩니다.
<br>
<b>header</b>에는 서명 암호화 알고리즘과 토큰 유형이 저장되고
<b>payload</b>에는 토큰을 통해 공개하고자 하는 내용이 저장됩니다.
<br>
이때, 저장되는 정보를 Claim이라고 하는데 Claim은 key-value로 이뤄진 한쌍의 정보를 말합니다.
<br>
<b>Claim</b>은 registed claim pulic claim, private claim으로 나뉩니다.
<br>
<b>signature</b>는 header와 payload를 부호화 시킨것에 서버가 지정한 secret key로 암호화 시켜 토큰을 변조하기 어렵게 하는 서명입니다.
<br>

</div>
</details>

<br>

# :newspaper: Reference

[JWT란](https://inpa.tistory.com/entry/WEB-%F0%9F%93%9A-JWTjson-web-token-%EB%9E%80-%F0%9F%92%AF-%EC%A0%95%EB%A6%AC)  
[oauth 클라이언트 권한 부여를 위한 jwt](https://www.ibm.com/docs/ko/was-liberty/base?topic=uocpao2as-json-web-token-jwt-oauth-client-authorization-grants)

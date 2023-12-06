# 레디스에서 왜 조인을 하시죠?

## 1.Redis Hash 사용
> 레디스 해시 데이터 구조는 여러개의 필드를 저장할 수 있다.
```bash
HSET user:1 username "user1" email "user1@example.com"
HSET user:2 username "user2" email "user2@example.com"

HSET post:1 title "Post 1" content "Content of post 1" author_id 1
HSET post:2 title "Post 2" content "Content of post 2" author_id 2
```
위와 같이 사용자 정보와 게시글을 저장할 때, **author_id** 필드를 지정해 주었다.<br/>아래와 같이 1번 게시글의 작성자를 얻을 수 있다.

```bash
HGET post:1 author_id
````
```bash
HGET user:1 username
HGET user:1 email
```

## 2. Lua script 사용
> 레디스 2.6 버전부터 Lua 5.1버전을 지원하기 시작했다. **eval** 사용
- Lua란?
    - 1993년 개발된 프로그래밍 언어
    - 가볍고 빠르며 문법이 단순한 인터프리터형 언어
    - 다양한 프로그램에 쉽게 이식 가능
- Lua in Redis
    - **eval** 명령어를 통해 Lua 스크립트를 redis에서 실행 가능
    - **script load** 명령어를 통해 Lua 스크립트를 redis에 등록 가능
    - Lua 스크립트 내에서 레디스 명령어 사용 가능
    - Lua 스크립트가 실행되는 동안 다른 레디스 명령 실행 불가능 -> 성능에 영향을 줄 수 있음
    - 전역변수를 사용하면 레디스 내 함수와 충돌할 수 있으므로 **지역변수**사용 권장

**Lua Script Example**
```bash
local userId = KEYS[1]
local postsKey = "user:" .. userId .. ":posts"
local postIds = redis.call("SMEMBERS", postsKey)
local posts = {}

for i, postId in ipairs(postIds) do
    local postKey = "post:" .. postId
    local title = redis.call("HGET", postKey, "title")
    local content = redis.call("HGET", postKey, "content")
    table.insert(posts, {title = title, content = content})
end

return cjson.encode(posts)
```
**1번 사용자가 작성한 게시글 목록 반환**
```bash
EVAL "lua 스크립트" 1 "1"
```

## 3. 외부 서비스에서 조인 처리
> Redis는 읽기 쓰기만 할 거야
- 필요한 데이터를 레디스에서 가져온 후, 외부 서비스에서 필요한 조인 로직을 처리
- 다만, 외부에서 처리할 때의 복잡성 및 성능을 고려해야 함

# 예상 질문
<details>
<summary>
레디스에서 조인을 사용할 수 있을까요?</summary>
<div markdown="1">
<b>레디스는 JOIN 연산을 지원하지 않고, 데이터를 키-값 형식으로 저장하여 빠른 읽기와 쓰기에 강점을 보입니다만은...<br/>굳이 사용하자면 Lua 스크립트를 사용하거나, redis에서 데이터를 검색 후 외부 서비스에서 조인 연산을 처리, 또는 레디스 해시 자료구조를 이요해 관계된 정보를 저장하는 필드를 같이 저장하여 여러 번 호출하는 방법이 있겠네요.</b>
</div>
</details>

# 레퍼런스
- [Lua 스크립트](https://bstar36.tistory.com/348)
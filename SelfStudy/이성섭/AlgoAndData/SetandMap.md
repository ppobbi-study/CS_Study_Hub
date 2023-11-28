# Set과 Map 자료구조

Set과 Map은 컴퓨터 프로그래밍에서 널리 사용되는 자료구조입니다:

## Map

키와 데이터를 같이 저장할 수 있는 구조

- 데이터를 저장, 검색, 수정할 때 키를 사용
  - python의 dict
  - java의 hashMap, Treemap
  - C++의 std::map

## Set

중복을 허용하지 않는 {"key" : "value"} 의 집합

- 요소의 유일성이 중요할 때 사용
  - python의 set
  - java의 HashSet, TreeSet
  - C++의 std::set

### Python

해시 테이블 기반.
순서를 보장하지 않음.
중복된 요소를 허용하지 않음.
일반적인 연산(삽입, 삭제, 멤버십 테스트)의 시간 복잡도는 평균적으로 O(1)이지만, 최악의 경우 O(n)이 될 수 있음.

### Java

Set 인터페이스는 여러 구현체를 가짐.
HashSet: 해시 테이블을 사용, 요소의 순서를 유지하지 않음.
TreeSet: 레드-블랙 트리를 사용, 요소가 정렬된 상태로 유지됨.
LinkedHashSet: 해시 테이블과 연결 리스트를 사용, 삽입 순서를 유지함.

### C++

균형 이진 검색 트리(보통 레드-블랙 트리)를 사용.
요소는 자동으로 정렬됨.
삽입, 삭제, 검색 등의 연산은 O(log n)의 시간 복잡도를 가짐.

# Reference

[자료구조](https://popo015.tistory.com/102)

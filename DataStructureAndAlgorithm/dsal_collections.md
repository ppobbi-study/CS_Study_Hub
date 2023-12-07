# Collections

## java.util.Collection vs java.util.Collections

-   Collection
    -   List, Set, Map 등이 이 인터페이스를 구현하거나 확장
    -   요소들을 추가, 제거, 검색할 수 있는 일반적인 메소드를 제공해 주는 템플릿 역할
-   Collections
    -   컬렉션들을 조작하기 위한 정적 메소드 지원
    -   binarySearch, sort등

## List

> 순서가 있는 컬렉션

-   사용자가 정수 index를 통해 요소의 위치를 정확하게 제어할 수 있음
-   일반적으로 중복 요소를 허용
-   동기화되지 않음 -> 여러 스레드가 하나의 List 인스턴스에 동시에 수정할 경우 문제 발생 가능

    -   `List list = Collections.synchronizedList(new ArrayList(...));`를 사용해 방지 가능

### ArrayList

> 배열을 사용한 List

-   size, isEmpty, get, set, iterator, listIterator의 연산은 상수 시간에 실행
-   add 연산은 amortized한 상수 시간에 실행 - 배열 크기를 늘려할 경우는 O(n)시간이 걸리지만 평균적으로는 O(1)의 시간이 걸림
    -   amortized time? - 특정 연산이 최악의 경우에 매우 느릴 수 있지만, 일반적으로 빠른 시간에 수행되는 경우에 유용한 시간 복잡도 분석방법
-   다른 연산들은 대략적으로 선형 시간을 가짐

### LinkedList

> double-linked list를 사용하여 List 인터페이스 구현

-   double-linked? - 양방향으로 연결되어 있는 리스트<br/>노드 탐색이 양쪽 모두 가능하다.<br/>단점으로는 앞의 노드를 지정하기 위한 메모리가 조그 더 필요하고 구현이 조금 복잡하다.

## Set

> 중복되는 원소가 없는 컬렉션

-   즉, e1.equals(e2)를 만족하는 (e1, e2)쌍이 존재하지 않는다.
-   null 요소도 많아야 하나 포함
-   값이 변경가능한(mutable) 객체, 특히 값의 변경이 객체 동등비교에 영향을 미치는 경우 주의가 필요 <- 이 경우 Set의 행동이 정의되어있지 않음

### SortedSet

> 원소에 대한 전체 정렬을 제공하는 Set

-   natural ordering을 사용하거나 SortedSet 생성 시점에 주어진 Comparator에 따라 정렬
-   SortedSet의 모든 요소는 Comparable 인터페이스를 구현하거나 Comparator에 따른 비교가 가능해야함

### HashSet

> Hash Table을 이용한 Set

-   요소들의 순서 보장 못함
-   null 허용
-   해시 함수가 적절할 경우, 기본 연산(add, remove, contains, size)에 상수 시간의 실행 보장

### TreeSet

> TreeMap기반의 NavigableSet 구현체

-   기본 작업(add, remove, contains)에 대해 log(n)시간 보장

### NavigableSet

> 탐색 대상에 가장 가까운 값을 주는 navigation 메소드를 확장한 SortedSet 인터페이스

-   오름차순 또는 내림차순으로 엑세스 및 순회가능
-   범위 검색에 높은 성능을 보임

## Map

# 예상 질문

-   collection과 collections의 차이가 뭘까요?
-   자바 컬렉션 중 아는 거 설명해보세요

# 레퍼런스

-   [Java Doc 11](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Collection.html)
-   [Armortized time](https://velog.io/@sapphire317/TIL3-Amortized-Time)

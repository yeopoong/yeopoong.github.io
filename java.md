Java
====

Java 8에 추가된 기능
-------------------

* 스트림 처리(Stream processing) 
* 동작 파라미터화(Behavior parameterization)로 메서드에 코드 전달하기
* 병렬성과 공유 가변 데이터(Shared mutable data)

동작 파라미터화 코드 전달하기
---------------------------

동작 파라미터화

람다 표현식
----------

람다란 무엇인가?

```java
Comparator<Apple> byWeight = (Apple al, Apple a2) -> a1.getWeight().compareTo(a2.getWeight());
```

함수형 데이터 처리
-----------------

* 스트림이란 무엇인가?
* 컬렉션과 스트림
* 내부 반복과 외부 반복
* 중간 연산과 최종 연산
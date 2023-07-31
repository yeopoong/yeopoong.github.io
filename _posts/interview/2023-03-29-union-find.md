---
layout: post
published: false
title: "Union Find"
categories: interview
tags: topics union-find
---

## Union Find

집합을 구현하는 데는 비트 벡터, 배열, 연결 리스트를 이용할 수 있으나 그 중 가장 효율적인 트리 구조를 이용하여 구현한다.  
아래의 세 가지 연산을 이용하여 Disjoint Set을 표현한다.

+ make-set(x)
  - 초기화
  - x를 유일한 원소로 하는 새로운 집합을 만든다.
+ union(x, y)
  - 합하기
  - x가 속한 집합과 y가 속한 집합을 합친다. 즉, x와 y가 속한 두 집합을 합치는 연산
+ find(x)
  - 찾기
  - x가 속한 집합의 대표값(루트 노드 값)을 반환한다. 즉, x가 어떤 집합에 속해 있는지 찾는 연산

## Disjoint Set
- 서로 중복되지 않는 부분 집합들로 나눠진 원소들에 대한 정보를 저장하고 조작하는 자료구조

[Medium]
- [990. Satisfiability of Equality Equations](/interview/2023/07/30/satisfiability-of-equality-equations/)
- [1101. The Earliest Moment When Everyone Become Friends](/interview/2023/05/21/the-earliest-moment-when-everyone-become-friends/)
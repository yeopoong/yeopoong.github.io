---
layout: post
published: true
title: "Bit Manipulation"
categories: interview
tags: topics bit-manipulation
---

> 비트 조작  
> - XOR 연산을 사용하면 여러개의 값 중에서 동일한 값들을 제거할 수 있다(동일한 값의 순서는 상관없다)  
> - XOR 연산으로 암호화 할 수 있다.  

Two bitmasks
```java
// 0 XOR A = A
// A XOR A = 0
int bitmask = 0;
for (int num : nums) bitmask ^= num;
```

[Easy]
- [136. Single Number](/interview/2023/04/26/single-number/)
- [190. Reverse Bits](/interview/2023/07/04//reverse-bits/)
- [191. Number of 1 Bits](/interview/2023/07/17/number-of-1-bits/)
- [338. Counting Bits](/interview/2023/08/20/counting-bits/)

[Medium]
- [260. Single Number III](/interview/2023/05/21/single-number-iii/)
---
layout: post
published: false
title: "Dynamic Programming"
categories: interview
tags: interview 
---

## Dynamic Programming

[Recursion]
재귀함수로 구현할 경우 반복해서 계산되는 부분이 존재하면 효율성이 떨어진다.

점화식(Recurrence relation): F(n) = F(n-1) + F(n-2)

[Memoization]
반복되는 부분을 캐슁(해서 실행속도를 증가시킬 수 있다.
하지만 재귀호출로 구현하게 되면 스택을 사용하게 되므로 재귀회수가 커질 경우 오버플로우가 발생할 수 있다.

[Dynamic Programming]
Bottom-Up 방식으로 반복을 이용해서 구현
상향식 방법으로 구현할 수 있다.

[Problem]
- [509. Fibonacci Number](https://leetcode.com/problems/fibonacci-number/)
- [70. Climbing Stairs](https://leetcode.com/problems/climbing-stairs)
- [746. Min Cost Climbing Stairs](https://leetcode.com/problems/min-cost-climbing-stairs)
- [198. House Robber](https://leetcode.com/problems/house-robber)
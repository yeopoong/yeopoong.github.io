---
layout: post
published: false
title: "Dynamic Programming"
categories: interview
tags: interview dynamic-programming
---

## Dynamic Programming
> 서브문제로 나눌 수 있으면 동적 프로그래밍으로 해결 가능하다.

Realizing a Dynamic Programming Problem  

This problem has two important attributes that let us know it should be solved by dynamic programming. 
- First, the question is asking for the maximum or minimum of something. 
- Second, we have to make decisions that may depend on previously made decisions, which is very typical of a problem involving subsequences.

A Framework to Solve Dynamic Programming Problems  
Typically, dynamic programming problems can be solved with three main components. If you're new to dynamic programming, this might be hard to understand but is extremely valuable to learn since most dynamic programming problems can be solved this way.

First, we need some function or array that represents the answer to the problem from a given state. For many solutions, you will see this function/array named "dp". 
For this problem, let's say that we have an array dp. As just stated, this array needs to represent the answer to the problem for a given state, so let's say that dp[i] represents the length of the longest increasing subsequence that ends with the ith element.
The "state" is one-dimensional since it can be represented with only one variable - the index i

Second, we need a way to transition between states, such as dp[5] and dp[7]. This is called a recurrence relation and can sometimes be tricky to figure out. Let's say we know dp[0], dp[1], and dp[2]. How can we find dp[3] given this information? Well, since dp[2] represents the length of the longest increasing subsequence that ends with nums[2], if nums[3] > nums[2], then we can simply take the subsequence ending at i = 2 and append nums[3] to it, increasing the length by 1. The same can be said for nums[0] and nums[1] if nums[3] is larger. Of course, we should try to maximize dp[3], so we need to check all 3. Formally, the recurrence relation is: dp[i] = max(dp[j] + 1) for all j where nums[j] < nums[i] and j < i.

The third component is the simplest: we need a base case. For this problem, we can initialize every element of dp to 1, since every element on its own is technically an increasing subsequence.

Usually, solving and fully understanding a dynamic programming problem is a 4 step process:

1. Start with the recursive backtracking solution
2. Optimize by using a memoization table (top-down[2] dynamic programming)
3. Remove the need for recursion (bottom-up dynamic programming)
4. Apply final tricks to reduce the time / memory complexity
All solutions presented below produce the correct result, but they differ in run time and memory requirements.

[Recursion]
재귀함수로 구현할 경우 반복해서 계산되는 부분이 존재하면 효율성이 떨어진다.

점화식(Recurrence relation): F(n) = F(n-1) + F(n-2)

[Memoization]
반복되는 부분을 캐슁(해서 실행속도를 증가시킬 수 있다.
하지만 재귀호출로 구현하게 되면 스택을 사용하게 되므로 재귀회수가 커질 경우 오버플로우가 발생할 수 있다.

[Dynamic Programming]
Bottom-Up 방식으로 반복을 이용해서 구현
상향식 방법으로 구현할 수 있다.

[Easy]
- [70. Climbing Stairs](https://leetcode.com/problems/climbing-stairs)
- [509. Fibonacci Number](https://leetcode.com/problems/fibonacci-number/)
- [746. Min Cost Climbing Stairs](https://leetcode.com/problems/min-cost-climbing-stairs)

[Medium]
- [53. Maximum Subarray](https://leetcode.com/problems/maximum-subarray/)
- [64. Minimum Path Sum](https://leetcode.com/problems/minimum-path-sum/)
- [139. Word Break](https://leetcode.com/problems/word-break/)
- [152. Maximum Product Subarray](https://leetcode.com/problems/maximum-product-subarray/)
- [198. House Robber](https://leetcode.com/problems/house-robber)
- [300. Longest Increasing Subsequence](https://leetcode.com/problems/longest-increasing-subsequence/) : 
- [673. Number of Longest Increasing Subsequence](https://leetcode.com/problems/number-of-longest-increasing-subsequence/)
- [322. Coin Change](https://leetcode.com/problems/coin-change/)
- [213. House Robber II](https://leetcode.com/problems/house-robber-ii/)
- [1143. Longest Common Subsequence](https://leetcode.com/problems/longest-common-subsequence/)
- [309. Best Time to Buy and Sell Stock with Cooldown](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/)
- [416. Partition Equal Subset Sum](https://leetcode.com/problems/partition-equal-subset-sum/)

[Hard]
- [42. Trapping Rain Water](https://leetcode.com/problems/trapping-rain-water/)
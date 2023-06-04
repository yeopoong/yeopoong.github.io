---
layout: post
published: true
title: "746. Min Cost Climbing Stairs"
categories: interview
tags: dynamic-programming
---

> cost[i]가 계단에서 i번째 단계의 비용인 정수 배열 비용이 주어집니다. 비용을 지불하면 한 단계 또는 두 단계를 오를 수 있습니다.  
> 정상에 도달하기 위한 최소 비용을 반환

- [746. Min Cost Climbing Stairs](https://leetcode.com/problems/min-cost-climbing-stairs)

```java
class Solution {
    // Dynamic Programming: 정상에 도달하기 위한 최소 비용
    // O(n)
    public int minCostClimbingStairs(int[] cost) {
        int length = cost.length;
        
        // Constraints: 계단이 3개이상 일 경우에 계산이 필요하다.
        for (int i = 2; i < length; i++) {
            // 앞의 두 계단에서 더 작은 값을 합산한다.
            cost[i] += Math.min(cost[i-1], cost[i-2]);
        }
        
        //System.out.println(Arrays.toString(cost));
                
        return Math.min(cost[length - 1], cost[length - 2]);
    }
}
```
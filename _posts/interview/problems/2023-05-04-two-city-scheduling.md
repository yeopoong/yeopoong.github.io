---
layout: post
published: true
title: "1029. Two City Scheduling"
categories: interview
tags: problems array sort greedy
---

> 정확히 n명이 각 도시에 도착하도록 모든 사람을 도시로 보내는 최소 비용을 반환

- [1029. Two City Scheduling](https://leetcode.com/problems/two-city-scheduling/)


```java
class Solution {
    // 정확히 n명이 각 도시에 도착하도록 모든 사람을 도시로 보내는 데 드는 최소 비용을 반환
    // T: O(nlogn)
    public int twoCitySchedCost(int[][] costs) {
        int total = 0;
        
        // 비용의 차이값 순으로 정렬
        Arrays.sort(costs, (a, b) ->  (a[1] - a[0]) - (b[1] - b[0]));
        
        int n = costs.length / 2;
        for (int i = 0; i < n; i++) { 
            // 앞절반(뒤) + 뒤절반(앞)
            total += costs[i][1] + costs[i + n][0];
        }
        
        return total;
    }
}
```

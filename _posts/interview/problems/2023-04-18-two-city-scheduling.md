---
layout: post
published: true
title: "1029. Two City Scheduling"
categories: interview
tags: problems greedy
---

> 정확히 n명이 각 도시에 도착하도록 모든 사람을 도시로 보내는 데 드는 최소 비용을 반환

- [1029. Two City Scheduling](https://leetcode.com/problems/two-city-scheduling/)

```java
class Solution {
    // 정확히 n명이 각 도시에 도착하도록 모든 사람을 도시로 보내는 데 드는 최소 비용을 반환
    // T: O(nlogn)
    public int twoCitySchedCost(int[][] costs) {
        int price = 0;
        
        Arrays.sort(costs, (a, b) -> {
            return (a[0] - a[1]) - (b[0] - b[1]);
        });
        
        for (int i = 0; i < costs.length / 2; i++) {
            price += costs[i][0];
        }
        
        for (int i = costs.length / 2; i < costs.length; i++) {
            price += costs[i][1];
        }
        
        return price;
    }
}
```
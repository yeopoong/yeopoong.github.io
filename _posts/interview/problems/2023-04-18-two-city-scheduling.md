---
layout: post
published: true
title: "1029. Two City Scheduling"
categories: interview
tags: problems array sort greedy
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

```java
class Solution {
    
    // 정확히 n명이 각 도시에 도착하도록 모든 사람을 도시로 보내는 데 드는 최소 비용을 반환
    // T: O(n^2)
    public int twoCitySchedCost(int[][] costs) {
        int N = costs.length / 2;
        
        int[][] dp = new int[N + 1][N + 1];
        
        for (int i = 1; i <= N; i++) {
            dp[i][0] = dp[i - 1][0] + costs[i - 1][0];
        }
        
        for (int j = 1; j <= N; j++) {
            dp[0][j] = dp[0][j - 1] + costs[j - 1][1];
        }
        
        for (int i = 1; i <= N; i++) {
            for (int j = 1; j <= N; j++) {
                dp[i][j] = Math.min(dp[i - 1][j] + costs[i + j - 1][0], dp[i][j - 1] + costs[i + j - 1][1]);
            }
        }
        
        return dp[N][N];
    }
}
```
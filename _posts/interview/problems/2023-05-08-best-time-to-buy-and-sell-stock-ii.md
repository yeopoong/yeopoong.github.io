---
layout: post
published: true
title: "122. Best Time to Buy and Sell Stock II"
categories: interview
tags: array 
---

> 달성할 수 있는 최대 이익을 찾아 반환

- [122. Best Time to Buy and Sell Stock II](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/)


```java
class Solution {
    
    // 달성할 수 있는 최대 이익
    // O(n)
    public int maxProfit(int[] prices) {
        int profit = 0;
        
        for (int i = 1; i < prices.length; i++) {
            // 증가구간이면 이윤이 발생한다.
            if (prices[i] > prices[i - 1]) {
                profit += (prices[i] - prices[i - 1]);
            }
        }

        return profit;
    }
}
```

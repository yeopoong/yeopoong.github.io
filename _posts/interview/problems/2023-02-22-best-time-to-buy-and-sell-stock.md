---
layout: post
published: true
title: "121. Best Time to Buy and Sell Stock"
categories: interview
tags: problems two-pointer
---

> 주식을 사고 팔기 가장 좋은 시기: the maximum profit

- [121. Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)

```java
class Solution {
    // 주식을 사고 팔기 가장 좋은 시기: the maximum profit
    // Two Pointer: Buy, Sell
    // 이익 = 현재가격 - 최소가격
    // O(n)
    public int maxProfit(int[] prices) {
        int maxProfit = 0;        // 최대이익
        
        int left = 0, right = 1;  // left=buy, right=sell
        
        while (right < prices.length) {
            // 왼쪽 값보다 크면 이익이 발생하므로 최대이익을 비교
            if (prices[left] < prices[right]) {
                maxProfit = Math.max(maxProfit, prices[right] - prices[left]);
            // 왼쪽 값보다 작으면 최소가격이므로 왼쪽포인터를 이동
            } else {
                left = right;
            }
            right += 1;
        }
        
        return maxProfit;
    }
}
```
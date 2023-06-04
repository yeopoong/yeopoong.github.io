---
layout: post
published: true
title: "714. Best Time to Buy and Sell Stock with Transaction Fee"
categories: interview
tags: array greedy
---

> 달성할 수 있는 최대 이익을 찾기. 원하는 만큼 거래를 완료할 수 있지만 각 거래에 대해 거래 수수료를 지불

- [714. Best Time to Buy and Sell Stock with Transaction Fee](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-transaction-fee/)

```java
class Solution {
    // 달성할 수 있는 최대 이익 찾기
    // 동시에 여러거래에 참여할 수 없다(다시 사기 전에 주식을 팔아야 한다).
    // T: O(n)
    public int maxProfit(int[] prices, int fee) {
        int cash = 0;
        
        int hold = -prices[0];
        
        for (int i = 1; i < prices.length; i++) {
            // sell our stock
            cash = Math.max(cash, hold + prices[i] - fee);
            // buy a stock
            hold = Math.max(hold, cash - prices[i]);
        }
        
        return cash;
    }
}
```
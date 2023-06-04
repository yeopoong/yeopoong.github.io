---
layout: post
published: true
title: "309. Best Time to Buy and Sell Stock with Cooldown"
categories: interview
tags: array greedy
---

> 달성할 수 있는 최대 이익을 찾으십시오. 다음 제한 사항과 함께 원하는 만큼 거래를 완료할 수 있습니다(즉, 주식의 한 주식을 여러 번 매수하고 매도).  
> 주식을 매도한 후 다음 날(즉, 쿨다운 하루) 주식을 살 수 없습니다.

- [309. Best Time to Buy and Sell Stock with Cooldown](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/)

```java
class Solution {
    
    // key = (i, buying), value = max profilt
    Map<String, Integer> dp = new HashMap<>();
    int[] prices;

    // 주식을 여러개 살 수 없고, 주식을 매도한 다음날 살 수 없다.
    // T: O(n)
    public int maxProfit(int[] prices) {
        this.prices = prices;
        return dfs(0, true);
    }

    // State: Buying or Selling
    // If Buy  -> i + 1
    // If Sell -> i + 2 (cooldonw one day)
    public int dfs(int i, boolean buying) {
        // Base case
        if (i >= prices.length) {
            return 0;
        }

        String key = i + "-" + buying;

        if (dp.containsKey(key)) {
            return dp.get(key);
        }

        int profit = Integer.MIN_VALUE;
        if (buying) {
            profit = dfs(i + 1, !buying) - prices[i];
        } else {
            profit = dfs(i + 2, !buying) + prices[i];
        }

        int cooldown = dfs(i + 1, buying);
        dp.put(key, Math.max(profit, cooldown));

        return dp.get(key);
    }
}
```
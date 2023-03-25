---
layout: post
published: false
title: "787. Cheapest Flights Within K Stops"
categories: interview
tags: interview graph
---

- [787. Cheapest Flights Within K Stops](https://leetcode.com/problems/cheapest-flights-within-k-stops/)

```java
class Solution {

    // src에서 dst까지 최대 k 정지로 가장 저렴한 가격
    // Time Complexity: O(k * n)
    // Space Complexity: O(n)
    public int findCheapestPrice(int n, int[][] flights, int src, int dst, int k) {
        // initialize an array with max value of size n
        int[] prices = new int[n];
        
        Arrays.fill(prices, Integer.MAX_VALUE);

        // price from source to source is always 0
        prices[src] = 0;

        for (int i = 0; i <= k; i++) {
            int[] temp = new int[n];
            temp = Arrays.copyOf(prices, prices.length);

            for (int j = 0; j < flights.length; j++) {
                int s = flights[j][0]; // from
                int d = flights[j][1]; // to
                int p = flights[j][2]; // price

                if (prices[s] == Integer.MAX_VALUE) continue;
                if (prices[s] + p < temp[d]) {
                    temp[d] = prices[s] + p;
                }
            }

            prices = temp;
        }

        if (prices[dst] != Integer.MAX_VALUE) {
            return prices[dst];
        } else {
            return -1;
        }
    }
}
```
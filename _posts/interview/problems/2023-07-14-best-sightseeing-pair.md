---
layout: post
published: true
title: "1014. Best Sightseeing Pair"
categories: interview
tags: medium dynamic-programming
---

> 한 쌍의 관광 명소의 최대 점수를 반환

[1014. Best Sightseeing Pair](https://leetcode.com/problems/best-sightseeing-pair/)

```java
class Solution {
    
    // T: O(n)
    public int maxScoreSightseeingPair(int[] values) {
        int res = 0, cur = 0;
        
        for (int a: values) {
            res = Math.max(res, cur + a);
            cur = Math.max(cur, a) - 1;
        }
        
        return res;
    }
}
```
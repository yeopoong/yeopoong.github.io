---
layout: post
published: true
title: "254. Factor Combinations"
categories: interview
tags: backtracking math
---

> 정수 n이 주어지면 인수의 가능한 모든 조합을 반환  
> - For example, 8 = 2 x 2 x 2 = 2 x 4.

[254. Factor Combinations](https://leetcode.com/problems/factor-combinations/)

```java
class Solution {
    
    List<List<Integer>> result = new ArrayList<>();
    List<Integer> item = new ArrayList<>();
    
    // 인수의 가능한 모든 조합
    public List<List<Integer>> getFactors(int n) {
        helper(n, 2);
        
        return result;
    }

    public void helper(int n, int start){
        if (n <= 1) {
            if (item.size() > 1) {
                result.add(new ArrayList<Integer>(item));
            }
            return;
        }

        for (int i = start; i <= n; ++i) {
            // 나머지가 0이면 인수
            if (n % i == 0) {
                item.add(i);
                helper(n/i, i);
                item.remove(item.size() - 1);
            }
        }
    }
}
```


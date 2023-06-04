---
layout: post
published: true
title: "39. Combination Sum"
categories: interview
tags: backtracking
---

> 배열에서 합이 타겟이 되는 조합 구하기: 같은 숫자가 여러번 선택될 수 있다.

- [39. Combination Sum](https://leetcode.com/problems/combination-sum/)

```java
class Solution {
    
    List<List<Integer>> list = new ArrayList<>();
    List<Integer> temp = new ArrayList<>();
    
    // 합이 타겟이 되는 조합 구하기: 같은 숫자가 여러번 선택될 수 있다.
    // Backtracking
    // T: O(2^target)
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        backtrack(candidates, target, 0);
        return list;
    }

    private void backtrack(int [] candidates, int remain, int start) {
        if (remain == 0) {
            list.add(new ArrayList<>(temp));
        }
        
        // 백트랙 조건 
        if (remain <= 0) return;
        
        for (int i = start; i < candidates.length; i++) {
            temp.add(candidates[i]);
            //The same number may be chosen from candidates an unlimited number of times. 
            //not i + 1 because we can reuse same elements
            backtrack(candidates, remain - candidates[i], i); 
            temp.remove(temp.size() - 1);
        }
    }
}
```
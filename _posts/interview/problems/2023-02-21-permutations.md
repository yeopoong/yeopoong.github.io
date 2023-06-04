---
layout: post
published: true
title: "46. Permutations"
categories: interview
tags: backtracking
---

> 개별 정수의 배열 숫자가 주어지면 가능한 모든 순열을 반환  
> - 정수 배열의 순열은 멤버를 시퀀스 또는 선형 순서로 배열

- [46. Permutations](https://leetcode.com/problems/permutations/solution/)

```java
class Solution {
    
    List<List<Integer>> list = new ArrayList<>();
    List<Integer> temp = new LinkedList<>();
    
    // 순열: Backtracking
    // Time complexity : O(n!)
    public List<List<Integer>> permute(int[] nums) {
       backtrack(nums, 0);
        
       return list;
    }

    private void backtrack(int[] nums, int i) {
    
        if (i == nums.length) {
            list.add(new ArrayList(temp));
            return;
        }

        //Insert elements in the array by increasing index
        for (int j = 0; j <= i; j++) {
            temp.add(j, nums[i]);
            backtrack(nums, i + 1);
            temp.remove(j);
        }
    }
}
```
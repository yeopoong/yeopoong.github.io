---
layout: post
published: true
title: "90. Subsets II"
categories: interview
tags: problems array backtracking
---

> 중복을 포함할 수 있는 정수 배열에서 가능한 모든 하위 집합을 반환

- [90. Subsets II](https://leetcode.com/problems/subsets-ii/)

```java
class Solution {
    List<List<Integer>> list = new ArrayList<>();
    List<Integer> temp = new ArrayList<>();
    
    // Backtracking
    // O(n*2^n)
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        // 중복 데이터가 존재하므로 중복체크를 하기 위해서 정렬한다.
        Arrays.sort(nums);
        
        backtraking(nums, 0);
        
        return list;
    }
    
    public void backtraking(int[] nums, int start) {
        list.add(new ArrayList<>(temp));
        
        for (int i = start; i < nums.length; i++) {
            //두번째 이후로 중복여부를 체크한다.
            if (i > start && nums[i] == nums[i - 1]) continue;
            
            temp.add(nums[i]);
            backtraking(nums, i + 1);     
            temp.remove(temp.size() - 1);
        }
    }
}
```

---
layout: post
published: true
title: "90. Subsets II"
categories: interview
tags: medium backtracking
---

> 중복을 포함할 수 있는 정수 배열 nums가 주어지면 가능한 모든 하위 집합을 반환

[90. Subsets II](https://leetcode.com/problems/subsets-ii/)

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

```java
class Solution {
    
    List<List<Integer>> list = new ArrayList<>();
    List<Integer> temp = new ArrayList<>();
    
    // Backtracking
    // O(n*2^n)
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        // 중복 데이터가 존재하므로 중복체크를 하기 위해서 정렬한다.
        Arrays.sort(nums);
        
        backtracking(nums, 0);
        
        return list;
    }
    
    // [[1,2,2],[1,2],[1],[2,2],[2],[]]
    public void backtracking(int[] nums, int i) {
        // 마지막 항목이면 결과 집합에 추가하고 종료
        if (i == nums.length) {
            list.add(new ArrayList<>(temp));
            return;
        }
        
        // 선택된 경우
        temp.add(nums[i]);
        backtracking(nums, i + 1);
        temp.remove(temp.size() - 1);
        
        // 중복 스킵
        while (i + 1 < nums.length && nums[i] == nums[i+1]) i += 1;
        
        // 선택안된 경우
        backtracking(nums, i + 1);
    }
}
```
---
layout: post
published: true
title: "445. Add Two Numbers II"
categories: interview
tags: problems linked-list
---

> 두 개의 음수가 아닌 정수를 나타내는 두 개의 비어 있지 않은 연결 목록이 제공됩니다. 가장 중요한 숫자가 먼저 나오고 각 노드에는 단일 숫자가 포함됩니다.  
> 두 숫자를 더하고 합계를 연결 리스트로 반환

- [445. Add Two Numbers II](https://leetcode.com/problems/add-two-numbers-ii/)

![](https://assets.leetcode.com/uploads/2021/04/09/sumii-linked-list.jpg)

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

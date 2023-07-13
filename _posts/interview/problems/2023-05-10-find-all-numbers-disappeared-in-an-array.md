---
layout: post
published: true
title: "448. Find All Numbers Disappeared in an Array"
categories: interview
tags: easy array hashmap
---

> nums[i]가 [1, n] 범위에 있는 n 정수의 배열 nums가 주어지면 [1, n] 범위에서 nums에 나타나지 않는 모든 정수의 배열을 반환

[448. Find All Numbers Disappeared in an Array](https://leetcode.com/problems/find-all-numbers-disappeared-in-an-array/)

후속 조치: 추가 공간 없이 O(n) 런타임에서 수행할 수 있습니까?

```java
class Solution {
    
    // 배열에서 사라진 모든 숫자 찾기: nums에 나타나지 않는 [1, n] 사이의 모든 정수의 목록을 리턴
    // T: O(n), S: O(1) 
    public List<Integer> findDisappearedNumbers(int[] nums) {
        List<Integer> res = new ArrayList<>();
        
        for (int i = 0; i < nums.length; i++) {
            int newIndex = Math.abs(nums[i]) - 1;
            
            // 아직 마킹되지 않았으면 음수로 마킹한다.
            if (nums[newIndex] > 0) {
                nums[newIndex] *= -1;
            }
        }
        
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] > 0) {
                res.add(i + 1);
            }
        }
        
        return res;
    }
}
```
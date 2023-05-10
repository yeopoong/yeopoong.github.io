---
layout: post
published: true
title: "448. Find All Numbers Disappeared in an Array"
categories: interview
tags: problems array hashmap
---

> nums[i]가 [1, n] 범위에 있는 n 정수의 배열 nums가 주어지면 [1, n] 범위에서 nums에 나타나지 않는 모든 정수의 배열을 반환

- [448. Find All Numbers Disappeared in an Array](https://leetcode.com/problems/find-all-numbers-disappeared-in-an-array/)

후속 조치: 추가 공간 없이 O(n) 런타임에서 수행할 수 있습니까?

```java
class Solution {
    
    // 배열에서 사라진 모든 숫자 찾기: nums에 나타나지 않는 모든 정수의 배열
    // n == nums.length
    // T: O(n), S: O(n) 
    public List<Integer> findDisappearedNumbers(int[] nums) {
        
        List<Integer> result = new ArrayList<>();
        
        Set<Integer> set = new HashSet<>();
        
        for (int num: nums) {
            set.add(num);
        }
        
        // 1부터 N까지 숫자중에 맵에 없는 숫자를 결과 리스트에 추가한다.
        for (int i = 1; i <= nums.length; i++) {
            if (!set.contains(i)) {
                result.add(i);
            }
        }
        
        return result;
    }
}
```
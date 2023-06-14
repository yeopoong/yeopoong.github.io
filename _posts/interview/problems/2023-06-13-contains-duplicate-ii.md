---
layout: post
published: true
title: "219. Contains Duplicate II"
categories: interview
tags: easy hashmap
---

> 정수 배열 nums와 정수 k가 주어지면 배열에 nums[i] == nums[j] 및 abs(i - j) <= k가 되는 두 개의 고유 인덱스 i와 j가 있으면 true를 반환

[219. Contains Duplicate II](https://leetcode.com/problems/contains-duplicate-ii/)

```java
class Solution {
    
    // 배열에서 K거리 이내에 중복된 값 찾기
    // T: O(1)
    public boolean containsNearbyDuplicate(int[] nums, int k) {
        Map<Integer, Integer> map = new HashMap<>();
	
        for (int i = 0; i <  nums.length; i++) {
            // 맵에 현재값을 키로해서 인덱스를 저장한다.
            Integer pre = map.put(nums[i], i);
            // 만약 중복된 값이 존재하면 인덱스 차이를 비교한다.
            if (pre != null && i - pre <= k) {
                return true;
            }
        }
	
	    return false;
    }
}
```

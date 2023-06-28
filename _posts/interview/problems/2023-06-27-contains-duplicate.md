---
layout: post
published: true
title: "217. Contains Duplicate"
categories: interview
tags: easy array
---

> 정수 배열 nums가 주어지면 값이 배열에 두 번 이상 나타나면 true를 반환하고 모든 요소가 고유하면 false를 반환

[217. Contains Duplicate](https://leetcode.com/problems/contains-duplicate/)

```java
class Solution {
    
    // 중복이 존재하는지 체크
    // T: O(n)
    public boolean containsDuplicate(int[] nums) {
        HashMap<Integer, Integer> map = new HashMap<>();
        for (int i : nums) {
            if (map.get(i) != null) {
                return true;
            } else {
                map.put(i, 0);
            }
        }
            
        return false;
    }
}
```
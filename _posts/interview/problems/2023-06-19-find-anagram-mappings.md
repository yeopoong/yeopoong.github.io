---
layout: post
published: true
title: "760. Find Anagram Mappings"
categories: interview
tags: easy hashmap
---

> 두 개의 정수 배열 nums1과 nums2에서 nums2는 nums1의 애너그램입니다. nums1에서 nums2로 매핑하는 인덱스 매핑 배열을 반환

[760. Find Anagram Mappings](https://leetcode.com/problems/find-anagram-mappings/)

```java
class Solution {
    
    // 숫자배열의 아나그램 매핑 찾기
    // T: O(n)
    public int[] anagramMappings(int[] nums1, int[] nums2) {
        // List to store the anagram mappings.
        int[] mappings = new int[nums1.length];
        
        // Store the index corresponding to the value in the second list.
        HashMap<Integer,Integer> map = new HashMap<>();
        
        // {value:index}
        for (int i = 0; i < nums2.length; i++) {
            map.put(nums2[i], i);
        }

        for (int i = 0; i < nums1.length; i++) {
            mappings[i]  = map.get(nums1[i]);
        }

        return mappings;
    }
}
```

---
layout: post
published: true
title: "2215. Find the Difference of Two Arrays"
categories: interview
tags: hashmap
---

> 두 개의 정수 배열 nums1 및 nums2가 주어지면 다음을 만족하는 리스트를 반환
> - answer[0]은 nums2에 없는 nums1의 모든 개별 정수 목록  
> - answer[1]은 nums1에 없는 nums2의 모든 개별 정수 목록

[2215. Find the Difference of Two Arrays](https://leetcode.com/problems/find-the-difference-of-two-arrays/)

```java
class Solution {
    
    // 두 배열의 차이 찾기
    public List<List<Integer>> findDifference(int[] nums1, int[] nums2) {
        return Arrays.asList(find(nums1, nums2), find(nums2, nums1));
    }
    
    // Returns the elements in the first arg nums1 that don't exist in the second arg nums2.
    List<Integer> find(int[] nums1, int[] nums2) {
        Set<Integer> result = new HashSet<>(); 
        
        Set<Integer> exists = new HashSet<>(); 
        for (int num : nums2) {
            exists.add(num);
        }
        
        for (int num : nums1) {
            if (!exists.contains(num)) {
                result.add(num);
            }
        }
        
        return new ArrayList<>(result);
    }
}
```

```java
class Solution {
    
    // 두 배열의 차이 찾기
    public List<List<Integer>> findDifference(int[] nums1, int[] nums2) {
        Set<Integer> s1 = Arrays.stream(nums1).boxed().collect(Collectors.toSet());
        Set<Integer> s2 = Arrays.stream(nums2).filter(n -> !s1.contains(n)).boxed().collect(Collectors.toSet());
        Arrays.stream(nums2).forEach(s1::remove);
        
        return Arrays.asList(new ArrayList<>(s1), new ArrayList<>(s2));
    }
}
```
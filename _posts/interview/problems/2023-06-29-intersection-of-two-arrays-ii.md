---
layout: post
published: true
title: "350. Intersection of Two Arrays II"
categories: interview
tags: easy two-pointers
---

> 두 개의 정수 배열 nums1과 nums2가 주어지면 교집합의 배열을 반환

[350. Intersection of Two Arrays II](https://leetcode.com/problems/intersection-of-two-arrays-ii/)

정렬 후에 각 배열의 값을 두개의 포인터를 이용해서 진행하면서 값을 비교하여 동일값이면 결과 집합에 추가한다.

```java
class Solution {
    
    // 두 배열의 교집합: 정렬 후에 각 배열의 값을 비교하면서 결과 집합을 만든다.
    // T: O(nlogn+mlogm)
    public int[] intersect(int[] nums1, int[] nums2) {
        ArrayList<Integer> result = new ArrayList<>();
        
        Arrays.sort(nums1);
        Arrays.sort(nums2);
        
        int p1 = 0, p2 = 0;
        
        while (p1 < nums1.length && p2 < nums2.length) {
            // 값을 비교해서 작은값의 배열 포인터를 증가 시킨다.
            if (nums1[p1] < nums2[p2]) {
                p1++;
            } else if (nums1[p1] > nums2[p2]) {
                p2++;
            } else {
                result.add(nums1[p1]);
                p1++;
                p2++;
            }
        }
        
        return result.stream().mapToInt(i -> i).toArray();
    }
}
```
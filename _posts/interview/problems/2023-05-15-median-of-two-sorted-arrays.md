---
layout: post
published: true
title: "4. Median of Two Sorted Arrays"
categories: interview
tags: array
---

> 크기가 각각 m과 n인 두 개의 정렬된 배열 nums1과 nums2가 주어지면 두 개의 정렬된 배열의 중앙값을 반환

- [4. Median of Two Sorted Arrays](https://leetcode.com/problems/median-of-two-sorted-arrays/)

```java
class Solution {
    
    // 정렬된 두 배열의 중앙값
    // T: O(log (m+n))
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        int m = nums1.length;
        int n = nums2.length;
        
        int[] merge = merge(nums1, nums2);
        
        // Even: m + n = 4 / 2 = 2
        // Odd:  m + n = 3 / 2 = 1
        if ((m+n) % 2 == 0) {
            return (double) (merge[(m+n)/2-1] + merge[(m+n)/2]) / 2;
        } else {
            return merge[(m+n)/2];
        }
    }
    
    private int[] merge(int[] nums1, int[] nums2) {
        int[] merge = new int[nums1.length + nums2.length];
        
        // 현재노드 포인터
        int p = 0, n1 = 0, n2 = 0;

        // 작은 노드를 P 노드에 연결 시킨다.
        while (n1 < nums1.length  && n2 < nums2.length) {
            if (nums1[n1] < nums2[n2]) {
                merge[p] = nums1[n1];
                n1++;
            } else {
                merge[p] = nums2[n2];
                n2++;
            }
            p++;
        }
        
        for (; n1 < nums1.length; n1++) merge[p++] = nums1[n1];
        for (; n2 < nums2.length; n2++) merge[p++] = nums2[n2];

        return merge; 
    }
}
```
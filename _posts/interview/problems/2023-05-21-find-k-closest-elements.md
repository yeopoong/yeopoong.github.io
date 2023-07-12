---
layout: post
published: true
title: "658. Find K Closest Elements"
categories: interview
tags: medium two-pointers
---

> 정렬된 정수 배열 arr, 두 정수 k 및 x가 주어지면 배열에서 x에 가장 가까운 k개의 정수를 반환

- [658. Find K Closest Elements](https://leetcode.com/problems/find-k-closest-elements/)

```java
class Solution {
    // 배열에서 x에 가장 가까운 k개의 정수
    // T: O(n)
    public List<Integer> findClosestElements(int[] arr, int k, int x) {
		List<Integer> result = new ArrayList<>(k);
        
        // Two Pointer
        int lo = 0, hi = arr.length - 1;
        
        // 구간의 원소의 개수가 K개가 될때까지 절대값을 비교하면서 두 구간의 위치를 변경한다.
		while (hi - lo + 1 > k) {
			if (Math.abs(arr[lo] - x) > Math.abs(arr[hi] - x)) {
				lo++;
			} else {
				hi--;
			}
		}
        
		for (int i = lo; i <= hi; i++) {
			result.add(arr[i]);
		}
        
		return result;
    }
}
```
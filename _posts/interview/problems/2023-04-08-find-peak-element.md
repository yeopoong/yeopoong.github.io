---
layout: post
published: true
title: "162. Find Peak Element"
categories: interview
tags: problems binary-search array
---

> 배열에서 피크 요소를 찾고 해당 인덱스를 반환  
> - A peak element is an element that is strictly greater than its neighbors.

- [162. Find Peak Element](https://leetcode.com/problems/find-peak-element/)

```java
class Solution {
    
    // 피크 요소 찾기
    // T: O(log n)
    // S: O(1)
    public int findPeakElement(int[] nums) {
        int left = 0, right = nums.length - 1;
        
        while (left < right) {
            int mid = left + (right - left) / 2;
            //다음값이 더 작으면 감소구간 이므로 최대값은 왼쪽에 존재한다.
            if (nums[mid] > nums[mid + 1]) {
                right = mid;
            //다음값이 더 크면 증가구간 이므로 최대값은 오른쪽에 존재한다.
            } else {
                left = mid + 1;
            }
        }
        
        return left;
    }
}
```
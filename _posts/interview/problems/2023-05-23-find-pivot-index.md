---
layout: post
published: true
title: "724. Find Pivot Index"
categories: interview
tags: array prefix-sum
---

> 정수 nums의 배열이 주어지면 이 배열의 피벗 인덱스를 계산합니다.

- [724. Find Pivot Index](https://leetcode.com/problems/find-pivot-index/)

```java
class Solution {
    
    // 가장 왼쪽 피벗 인덱스를 반환합니다. 해당 인덱스가 없으면 -1을 반환합니다.
    // left - pivot - right
    // T: O(n)
    public int pivotIndex(int[] nums) {
        int sum = 0, leftsum = 0;
        
        for (int x: nums) sum += x;
        
        for (int i = 0; i < nums.length; ++i) {
            // sum = leftsum + nums[i] + leftsum
            if (leftsum == sum - leftsum - nums[i]) {
                return i;
            } else {
                leftsum += nums[i];
            }
        }
        
        return -1;
    }
}
```
---
layout: post
published: true
title: "16. 3Sum Closest"
categories: interview
tags: array two-pointers
---

> 타겟에 가장 가까운 세 정수의 합

- [16. 3Sum Closest](https://leetcode.com/problems/3sum-closest/)

배열에서 3개의 숫자를 처리해야 하는 경우 정렬 후에 처음부터 루프를 돌면서 두개의 숫자를 Two Pointers 로 증감시키면서 처리한다.

```java
class Solution {
    // Two Pointer & Sliding Window
    // 타겟에 가장 가까운 세 정수의 합
    public int threeSumClosest(int[] nums, int target) {
        // 초기값
        int result = nums[0] + nums[1] + nums[nums.length - 1];
        
        Arrays.sort(nums);
        
        for (int i = 0; i < nums.length - 2; i++) {
            // Two Pointer
            int start = i + 1, end = nums.length - 1;
            
            while (start < end) {
                int sum = nums[i] + nums[start] + nums[end];
                
                // 결과값이 타켓과 더 가까우면(차이값의 절대값이 작으면) 갱신한다.
                if (Math.abs(sum - target) < Math.abs(result - target)) {
                    result = sum;
                }
                
                if (sum > target) end--;
                else if (sum < target) start++;
                else return result;
            }
        }
        
        return result;
    }
}
```

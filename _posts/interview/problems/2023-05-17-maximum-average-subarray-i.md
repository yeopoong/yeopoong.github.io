---
layout: post
published: true
title: "643. Maximum Average Subarray I"
categories: interview
tags: array sliding-window
---

> 길이가 k와 같고 평균값이 최대인 연속된 하위 배열을 찾아 이 값을 반환

- [643. Maximum Average Subarray I](https://leetcode.com/problems/maximum-average-subarray-i/)

```java
class Solution {
    
    // 최대 평균 하위 배열
    // T: O(n)
    public double findMaxAverage(int[] nums, int k) {
        double sum = 0;
        
        // 처음 K까지의 총합을 구한다.
        for (int i = 0; i < k; i++) {
            sum += nums[i];
        }
        
        double res = sum;
        
        // 슬라이딩 윈도우로 진행하면서
        for (int i = k; i < nums.length; i++) {
            // 다음값을 추가하고 처음값을 제외한다.
            sum += nums[i] - nums[i-k];
            // 최대값과 비교한다.
            res = Math.max(res, sum);
        }
        
        // 평균값을 리턴한다.
        return res / k;
    }
}
```
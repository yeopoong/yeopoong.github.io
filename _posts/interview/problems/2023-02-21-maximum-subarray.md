---
layout: post
published: true
title: "53. Maximum Subarray"
categories: interview
tags: problems dynamic-programming
---

> 합이 가장 큰 하위 배열을 찾아 그 합을 반환

- [53. Maximum Subarray](https://leetcode.com/problems/maximum-subarray/)

```java
import java.util.Collections;

class Solution {
    
    // Sliding Window: remove negative prefix
    // T: O(n)
    public int maxSubArray(int[] nums) {
        // 초기값은 처음값으로 설정
        int max = nums[0];
       
        int sum = 0;
        
        for (int num : nums) {
            sum += num ;
            // 현재까지의 합과 최대값을 비교
            max = Math.max(max, sum);
            // 합이 음수가 되면 이전까지 합은 사용될 필요가 없으므로 초기화 하고 다시 시작 한다. 
            if (sum < 0) sum = 0;
        }
        
        return max;
    }
}
```
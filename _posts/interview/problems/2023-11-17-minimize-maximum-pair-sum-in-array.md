---
layout: post
published: true
title: "1877. Minimize Maximum Pair Sum in Array"
categories: interview
tags: medium two-pointers
---

> 요소를 최적으로 쌍으로 묶은 후 최소화된 최대 쌍 합계를 반환
> - nums의 각 요소는 정확히 한 쌍으로 구성
> - 최대 쌍 합계가 최소화

[1877. Minimize Maximum Pair Sum in Array](https://leetcode.com/problems/minimize-maximum-pair-sum-in-array/)

![](https://leetcode.com/problems/minimize-maximum-pair-sum-in-array/Figures/1877/1877A.png)

```java
class Solution {
    // 배열의 최대 쌍 합계 최소화
    public int minPairSum(int[] nums) {
        // Step 1: Sort the array in ascending order
        Arrays.sort(nums);

        // Step 2: Initialize pointers at the start and end of the sorted array
        int left = 0, right = nums.length - 1;

        // Step 3: Initialize a variable to store the minimum of the maximum pair sum
        int minMaxPairSum = Integer.MIN_VALUE;

        // Step 4: Iterate until the pointers meet
        while (left < right) {
            // Step 5: Calculate the current pair sum
            int currentPairSum = nums[left] + nums[right];

            // Step 6: Update the minimum of the maximum pair sum
            minMaxPairSum = Math.max(minMaxPairSum, currentPairSum);

            // Step 7: Move the pointers towards the center
            left++;
            right--;
        }

        // Step 8: Return the minimum of the maximum pair sum
        return minMaxPairSum;
    }
}
```
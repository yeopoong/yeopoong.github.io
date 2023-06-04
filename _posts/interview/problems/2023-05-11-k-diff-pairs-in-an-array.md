---
layout: post
published: true
title: "532. K-diff Pairs in an Array"
categories: interview
tags: array two-pointer
---

> 정수 nums와 정수 k의 배열이 주어지면 배열에서 고유한 k-diff 쌍의 수를 반환

- [532. K-diff Pairs in an Array](https://leetcode.com/problems/k-diff-pairs-in-an-array/)

```java
class Solution {
    
    // T: O(nlogn)
    public int findPairs(int[] nums, int k) {
        int result = 0;
        
        Arrays.sort(nums);

        int left = 0, right = 1;

        while (left < nums.length && right < nums.length) {
            if (left == right || nums[right] - nums[left] < k) {
                // List item 1 in the text
                right++;      
            } else if (nums[right] - nums[left] > k) {
                // List item 2 in the text
                left++;       
            } else {
                // List item 3 in the text
                left++;
                result++;
                while (left < nums.length && nums[left] == nums[left - 1]) {
                    left++;
                }
            }
        }
        
        return result;
    }
}
```
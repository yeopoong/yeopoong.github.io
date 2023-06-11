---
layout: post
published: true
title: "532. K-diff Pairs in an Array"
categories: interview
tags: medium array two-pointer
---

> 정수 배열과 정수 k값이 주어지면 배열에서 두 수의 차이의 절대값이 K인 쌍의 개수를 반환  
> - 0 <= i, j < nums.length  
> - i != j  
> - |nums[i] - nums[j]| == k  

[532. K-diff Pairs in an Array](https://leetcode.com/problems/k-diff-pairs-in-an-array/)

정렬 후에 Two Pointer
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

HashMap
```java
class Solution {
    
    // T: O(n)
    public int findPairs(int[] nums, int k) {
        int result = 0;

        HashMap <Integer,Integer> counter = new HashMap<>();
        for (int n: nums) {
            counter.put(n, counter.getOrDefault(n, 0) + 1);
        }

        for (Map.Entry <Integer, Integer> entry: counter.entrySet()) {
            int x = entry.getKey();
            int val = entry.getValue();
            // 보수값이 존재하는지 체크
            if (k > 0 && counter.containsKey(x + k)) {
                result++;
            // K = 0 인 경우는 중복값이 존재하는지 체크
            } else if (k == 0 && val > 1) {
                result++;
            }
        }
        
        return result;
    }
}
```

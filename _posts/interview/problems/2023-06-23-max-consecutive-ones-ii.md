---
layout: post
published: true
title: "487. Max Consecutive Ones II"
categories: interview
tags: medium sliding-window
---

> 이진 배열 nums가 주어지면 최대 하나의 0을 뒤집을 수 있는 경우 배열에서 연속된 1의 최대 수를 반환

[487. Max Consecutive Ones II](https://leetcode.com/problems/max-consecutive-ones-ii/)

Sliding Window
```java
class Solution {
    public int findMaxConsecutiveOnes(int[] nums) {
        int longestSequence = 0;
        
        int left = 0;
        int right = 0;
        
        int numZeroes = 0;

        while (right < nums.length) {

            // add the right most element into our window
            if (nums[right] == 0) {
                numZeroes++;
            }

            // if our window is invalid, contract our window
            while (numZeroes == 2) {
                if (nums[left] == 0) {
                    numZeroes--;
                }
                left++;
            }

            // update our longest sequence answer
            longestSequence = Math.max(longestSequence, right - left + 1);

            // expand our window
            right++;
        }
        
        return longestSequence;
    }
}
```

Brute Force
```java
class Solution {
    
    public int findMaxConsecutiveOnes(int[] nums) {
        int longestSequence = 0;
        
        for (int left = 0; left < nums.length; left++) {
            int numZeroes = 0;

            // check every consecutive sequence
            for (int right = left; right < nums.length; right++) {
                // count how many 0's
                if (nums[right] == 0) {
                    numZeroes += 1;
                }
                // # update answer if it's valid
                if (numZeroes <= 1) {
                    longestSequence = Math.max(longestSequence, right - left + 1);
                }
            }
        }
        
        return longestSequence;
    }
}
```


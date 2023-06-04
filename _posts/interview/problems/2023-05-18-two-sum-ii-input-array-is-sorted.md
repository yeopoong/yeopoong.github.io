---
layout: post
published: true
title: "167. Two Sum II - Input Array Is Sorted"
categories: interview
tags: array two-pointers
---

> 정렬된 배열의 투썸: Two Pointer

- [167. Two Sum II - Input Array Is Sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/)

```java
class Solution {
    // 정렬된 배열의 투썸: Two Pointer
    // T: O(n)
    public int[] twoSum(int[] numbers, int target) {
        int[] result = new int[2];
        
        int first = 0, last = numbers.length - 1;
        
        while (first < last) {
            int sum = numbers[first] + numbers[last];
            
            if (sum == target) {
                result[0] = first + 1;
                result[1] = last + 1;
                break;
            }
            
            if (sum < target) {
                first += 1;
            } else {
                last -= 1;
            }
        }
        
        return result;
    }
}
```
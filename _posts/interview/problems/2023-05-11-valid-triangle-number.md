---
layout: post
published: true
title: "611. Valid Triangle Number"
categories: interview
tags: problems array
---

> 정수 배열 nums가 주어지면, 삼각형을 만들 수 있는 배열에서 선택한 삼중 항의 수를 반환

- [611. Valid Triangle Number](https://leetcode.com/problems/valid-triangle-number/)

```java
class Solution {
    
    // 유효한 삼각형 숫자
    // T: O(n^3)
    public int triangleNumber(int[] nums) {
        int count = 0;
        
        for (int i = 0; i < nums.length - 2; i++) {
            for (int j = i + 1; j < nums.length - 1; j++) {
                for (int k = j + 1; k < nums.length; k++) {
                    if (nums[i] + nums[j] > nums[k] && 
                        nums[i] + nums[k] > nums[j] && 
                        nums[j] + nums[k] > nums[i]) {
                        count++;
                    }
                }
            }
        }
        
        return count;
    }
}
```

```java
class Solution {
    
    // 유효한 삼각형 숫자
    // T: O(n^2)
    public int triangleNumber(int[] nums) {
        int count = 0;
        
        Arrays.sort(nums);
        for (int i = 0; i < nums.length - 2; i++) {
            int k = i + 2;
            for (int j = i + 1; j < nums.length - 1 && nums[i] != 0; j++) {
                while (k < nums.length && nums[i] + nums[j] > nums[k]) {
                    k++;
                }
                count += k - j - 1;
            }
        }
        
        return count;
    }
}
```
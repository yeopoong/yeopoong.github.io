---
layout: post
published: true
title: "503. Next Greater Element II"
categories: interview
tags: medium array stack
---

> 순환 정수 배열 nums가 주어지면(즉, nums[nums.length - 1]의 다음 요소는 nums[0]임) nums의 모든 요소에 대해 다음으로 큰 숫자를 반환

- [503. Next Greater Element II](https://leetcode.com/problems/next-greater-element-ii/)

Brute Force
```java
 class Solution {
    public int[] nextGreaterElements(int[] nums) {
        int[] res = new int[nums.length];
        
        for (int i = 0; i < nums.length; i++) {
            res[i] = -1;
            for (int j = 1; j < nums.length; j++) {
                if (nums[(i + j) % nums.length] > nums[i]) {
                    res[i] = nums[(i + j) % nums.length];
                    break;
                }
            }
        }
        
        return res;
    }
}
```

Using Stack
```java
class Solution {
    
    // 순환배열에서 다음으로 큰 수 찾기
    // T: O(n^2)
    public int[] nextGreaterElements(int[] nums) {
        int[] res = new int[nums.length];
        
        Stack<Integer> stack = new Stack<>();
        
        for (int i = 2 * nums.length - 1; i >= 0; --i) {
            while (!stack.empty() && nums[stack.peek()] <= nums[i % nums.length]) {
                stack.pop();
            }
            res[i % nums.length] = stack.empty() ? -1 : nums[stack.peek()];
            stack.push(i % nums.length);
        }
        
        return res;
    }
}
```

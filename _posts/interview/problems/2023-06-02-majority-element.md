---
layout: post
published: true
title: "169. Majority Element"
categories: interview
tags: problems design
---

> 크기 n의 배열 숫자가 주어지면 다수 요소를 반환

- [169. Majority Element](https://leetcode.com/problems/majority-element/)

```java
class Solution {
    // 과반수 요소 찾기
    // T: O(n)
    // S: O(1)
    public int majorityElement(int[] nums) {
        int major = 0;
        
        int count = 0;
        for (int num: nums) {
            if (count == 0) {
                major = num;
            }
            
            if (major == num) {
                count++;
            } else {
                count--;
            }
        }
        
        return major;
    }
}
```

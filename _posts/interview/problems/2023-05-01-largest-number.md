---
layout: post
published: true
title: "179. Largest Number"
categories: interview
tags: problems sort array
---

> 음이 아닌 정수 목록에서 가장 큰 수를 형성하도록 배열

- [179. Largest Number](https://leetcode.com/problems/largest-number/)

```java
class Solution {
    
    // 음이 아닌 정수 nums 목록이 주어지면 가장 큰 수를 형성하도록 배열
    public String largestNumber(int[] nums) {
        
        String[] result = new String[nums.length];

        for (int i = 0; i < nums.length; i++) {
            result[i] = String.valueOf(nums[i]);
        }

        Arrays.sort(result, (s1, s2) -> (s2 + s1).compareTo(s1 + s2));

        if (result[0].equals("0")) return "0";

        StringBuilder sb = new StringBuilder();
        for (String s : result) {
            sb.append(s);
        }

        return sb.toString();
    }
}
```

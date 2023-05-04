---
layout: post
published: true
title: "835. Image Overlap"
categories: interview
tags: problems array matrix
---

> 정수 배열 arr이 주어지면 arr의 최대 크기 난류 하위 배열의 길이를 반환

- [835. Image Overlap](https://leetcode.com/problems/image-overlap/)

```java
class Solution {
    public int maxTurbulenceSize(int[] arr) {
        int ans = 1;
        
        int anchor = 0;

        for (int i = 1; i < arr.length; ++i) {
            int c = Integer.compare(arr[i-1], arr[i]);
            if (c == 0) {
                anchor = i;
            } else if (i == arr.length-1 || c * Integer.compare(arr[i], arr[i+1]) != -1) {
                ans = Math.max(ans, i - anchor + 1);
                anchor = i;
            }
        }

        return ans;
    }
}
```

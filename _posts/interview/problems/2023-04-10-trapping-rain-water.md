---
layout: post
published: true
title: "42. Trapping Rain Water"
categories: interview
tags: two-pointers
---

> 각 막대의 너비가 1인 고도 지도를 나타내는 n개의 음이 아닌 정수가 주어지면 비가 내린 후 얼마나 많은 물을 가둘 수 있는지 계산

- [42. Trapping Rain Water](https://leetcode.com/problems/trapping-rain-water)

```java
class Solution {
    // 빗물 가두기
    // O(n)
    public int trap(int[] height) {
        int water = 0;

        // Two Pointers
        int l = 0, r = height.length - 1;
        
        // 양쪽 끝의 최대 높이
        int maxL = height[l], maxR = height[r];

        while (l < r) {
            // 작은 막대를 이동하고 해당 막대의 길이를 최대길이와 비교한다.
            if (maxL < maxR) {
                l++;
                maxL = Math.max(maxL, height[l]);
                water += maxL - height[l]; // 해당위치의 깊이 만큼 증가
            } else {
                r--;
                maxR = Math.max(maxR, height[r]);
                water += maxR - height[r]; // 해당위치의 깊이 만큼 증가 
            }
        }
        
        return water;
    }
}
```
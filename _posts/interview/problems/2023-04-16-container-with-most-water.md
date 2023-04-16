---
layout: post
published: true
title: "11. Container With Most Water"
categories: interview
tags: problems two-pointer array
---

> 용기가 저장할 수 있는 최대 물의 양을 반환

- [11. Container With Most Water](https://leetcode.com/problems/container-with-most-water/)

```java
class Solution {
    
    // BRUTE FORCE: O(n^2)
    public int maxArea(int[] height) {
        int maxWater = 0, water = 0;
        
        for (int left = 0; left < height.length; left++) {
            for (int right = 0; right < height.length; right++) {
                // * 면적(Area) = 가로(Width) * 세로(Height: 최소값)
                water = (right - left) * Math.min(height[left], height[right]);
                maxWater = Math.max(maxWater, water);
            }
        }
                    
        return maxWater;
    }
}
```

```java
class Solution {
    
    // Two Pointer: O(n)
    public int maxArea(int[] height) {
        int maxWater = 0, water = 0;
        
        // Two Pointer
        int left = 0, right = height.length - 1;
        
        while (left < right) {
            // 면적(Area) = 가로(Width) * 세로(Height: 최소값)
            water = (right - left) * Math.min(height[left], height[right]);
            maxWater = Math.max(maxWater, water);
            
            // 높이가 더 작은쪽은 이동한다.
            if (height[left] < height[right]) {
                left++;
            } else {
                right--;
            }
        }
                    
        return maxWater;
    }
}
```
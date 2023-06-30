---
layout: post
published: true
title: "11. Container With Most Water"
categories: interview
tags: medium two-pointers
---

> 용기가 저장할 수 있는 최대 물의 양을 반환

[11. Container With Most Water](https://leetcode.com/problems/container-with-most-water/)

![](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/07/17/question_11.jpg)

Brute Force
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

Two Pointer
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

```scala
object Solution {
    def maxArea(height: Array[Int]): Int = {
        var water = 0
        
        var left = 0
        var right = height.length - 1
        
        while (left < right) {
            var curr_water = (right - left) * Math.min(height(left), height(right))
            water = Math.max(water, curr_water)
            if (height(left) < height(right)) {
                left += 1
            } else {
                right -= 1
            }
        } 
        
        water
    }
}
```
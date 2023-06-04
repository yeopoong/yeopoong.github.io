---
layout: post
published: true
title: "1732. Find the Highest Altitude"
categories: interview
tags: array prefix-sum
---

> 가장 높은 고도 찾기

- [1732. Find the Highest Altitude](https://leetcode.com/problems/find-the-highest-altitude/)

```java
class Solution {
    
    // 가장 높은 고도 찾기
    // T: O(n)
    public int largestAltitude(int[] gain) {
        int currentAltitude = 0;
        
        // Highest altitude currently is 0.
        int highestPoint = currentAltitude;

        for (int altitudeGain : gain) {
          // Adding the gain in altitude to the current altitude.
          currentAltitude += altitudeGain;
          // Update the highest altitude.
          highestPoint = Math.max(highestPoint, currentAltitude);
        }

        return highestPoint;
    }
}
```
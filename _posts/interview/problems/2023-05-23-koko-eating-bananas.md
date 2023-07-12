---
layout: post
published: true
title: "875. Koko Eating Bananas"
categories: interview
tags: medium array binary-search
---

> h시간 내에 모든 바나나를 먹을 수 있는 최소 정수 k를 반환

- [875. Koko Eating Bananas](https://leetcode.com/problems/koko-eating-bananas/)

```java
class Solution {
    
    // h시간 내에 모든 바나나를 먹을 수 있는 최소 정수 k
    public int minEatingSpeed(int[] piles, int h) {
        int left = 1, right = 1;
        
        for (int pile : piles) {
            right = Math.max(right, pile);
        }

        while (left < right) {
            // Get the middle index between left and right boundary indexes.
            // hourSpent stands for the total hour Koko spends.
            int middle = (left + right) / 2;
            int hourSpent = 0;

            // Iterate over the piles and calculate hourSpent.
            // We increase the hourSpent by ceil(pile / middle)
            for (int pile : piles) {
                hourSpent += Math.ceil((double) pile / middle);
            }

            // Check if middle is a workable speed, and cut the search space by half.
            if (hourSpent <= h) {
                right = middle;
            } else {
                left = middle + 1;
            }
        }

        // Once the left and right boundaries coincide, we find the target value,
        // that is, the minimum workable eating speed.
        return right;
    }
}
```
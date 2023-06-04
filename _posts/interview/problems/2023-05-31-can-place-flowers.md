---
layout: post
published: true
title: "605. Can Place Flowers"
categories: interview
tags: array greedy
---

> 0과 1을 포함하는 정수 배열 화단이 주어지면 0은 비어 있음을 의미하고 1은 비어 있지 않음을 의미  
> 인접 꽃 없음 규칙을 위반하지 않고 n개의 새 꽃을 화단에 심을 수 있으면 true를 반환하고 그렇지 않으면 false를 반환

- [605. Can Place Flowers](https://leetcode.com/problems/can-place-flowers/)

```java
class Solution {
    public boolean canPlaceFlowers(int[] flowerbed, int n) {
        int count = 0;
        
        for (int i = 0; i < flowerbed.length && count < n; i++) {
            if (flowerbed[i] == 0) {
	            //get next and prev flower bed slot values. If i lies at the ends the next and prev are considered as 0. 
                int next = (i == flowerbed.length - 1) ? 0 : flowerbed[i + 1]; 
                int prev = (i == 0) ? 0 : flowerbed[i - 1];
                if (next == 0 && prev == 0) {
                    flowerbed[i] = 1;
                    count++;
                }
            }
        }
        
        return count == n;
    }
}
```

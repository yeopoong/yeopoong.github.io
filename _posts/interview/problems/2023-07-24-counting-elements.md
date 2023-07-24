---
layout: post
published: true
title: "1426. Counting Elements"
categories: interview
tags: easy hashmap
---

> 정수 배열이 주어지면 x + 1이 존재하는 x의 개수는?  
> arr에 중복 항목이 있는 경우 별도로 계산

[1426. Counting Elements](https://leetcode.com/problems/counting-elements/)

```java
class Solution {
    
    // T: O(n)
    public int countElements(int[] arr) {
        int count = 0;
        
        Set<Integer> set = new HashSet<>();
        
        for (int x : arr) {
            set.add(x);
        }
        
        for (int x : arr) {
            if (set.contains(x + 1)) {
                count++;
            }
        }
        
        return count;
    }
}
```
---
layout: post
published: true
title: "1492. The kth Factor of n"
categories: interview
tags: medium math
---

> 오름차순으로 정렬된 n의 모든 인수 목록에서 k번째 요소를 반환하거나 n의 요소가 k보다 작으면 -1을 반환

[1492. The kth Factor of n](https://leetcode.com/problems/the-kth-factor-of-n/)

```java
class Solution {
    
    // T: O(n)
    public int kthFactor(int n, int k) {
        for (int i = 1; i < n / 2 + 1; ++i) {
            if (n % i == 0) {
                --k;
                if (k == 0) {
                    return i;    
                }    
            }    
        }
        
        return k == 1 ? n : -1;
    }
}
```
---
layout: post
published: true
title: "978. Longest Turbulent Subarray"
categories: interview
tags: array longest sliding-window
---

> 정수 배열 arr이 주어지면 arr의 최대 크기 난류 하위 배열의 길이를 반환
> - 하위 배열의 인접한 각 요소 쌍 사이에서 비교 기호가 뒤집힌 하위 배열

- [978. Longest Turbulent Subarray](https://leetcode.com/problems/longest-turbulent-subarray/)

```java
class Solution {
    
    // 정수 배열 arr이 주어지면 arr의 최대 크기 난류 하위 배열의 길이를 반환
    // Sliding Window
    // T: O(n)
    public int maxTurbulenceSize(int[] arr) {
        int ans = 1;
        
        int anchor = 0;

        for (int i = 1; i < arr.length; ++i) {
            int c = Integer.compare(arr[i-1], arr[i]);
            if (c == 0) {
                anchor = i;
            // 마지막 인덱스 이거나 비교부호가 뒤집히지 않았으면: 
            } else if (i == arr.length - 1 || c * Integer.compare(arr[i], arr[i+1]) != -1) { 
                // 최대크기를 비교해서 갱신한다.
                ans = Math.max(ans, i - anchor + 1);
                // 최대크기를 초기화 한다.
                anchor = i;
            }
        }

        return ans;
    }
}
```

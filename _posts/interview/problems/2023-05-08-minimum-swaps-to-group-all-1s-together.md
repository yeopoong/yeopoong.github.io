---
layout: post
published: true
title: "1151. Minimum Swaps to Group All 1's Together"
categories: interview
tags: problems linked-list
---

> 바이너리 배열 데이터가 주어지면 배열의 모든 위치에서 배열에 있는 모든 1을 함께 그룹화하는 데 필요한 최소 스왑 수를 반환

- [1151. Minimum Swaps to Group All 1's Together](https://leetcode.com/problems/minimum-swaps-to-group-all-1s-together/)


```java
class Solution {
    
    // 배열에 있는 모든 1을 함께 그룹화하는 데 필요한 최소 스왑 수
    // T: O(n), S: O(1)
    public int minSwaps(int[] data) {
        int totalOne = Arrays.stream(data).sum();
        
        // 최소 스왑을 구해야 하므로 최대 1의 개수를 알면 된다.
        int maxOne = 0;
        int curOne = 0;
        
        int left = 0, right = 0;
        while (right < data.length) {
            // updating the number of 1's by adding the new element
            curOne += data[right++];
            
            // 윈도우 사이즈가 총 1의 개수보다 크면 왼쪽 포인터를 이동하고 1의 개수를 감소시킨다.
            if (right - left > totalOne) {
                // updating the number of 1's by removing the oldest element
                curOne -= data[left++];
            }
            
            // record the maximum number of 1's in the window
            maxOne = Math.max(maxOne, curOne);
        }
        
        return totalOne - maxOne;
    }
}
```

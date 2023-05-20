---
layout: post
published: true
title: "134. Gas Station"
categories: interview
tags: problems array greedy
---

> 두 개의 정수 배열 가스와 비용이 주어지면 시계 방향으로 한 바퀴를 돌 수 있으면 시작 주유소의 인덱스를 반환하고 그렇지 않으면 -1을 반환

- [134. Gas Station](https://leetcode.com/problems/gas-station/)

```java
class Solution {
    
    // 시계 방향으로 한 바퀴를 돌 수 있으면 시작 주유소의 인덱스를 반환
    // Greedy
    // T: O(n)
    public int canCompleteCircuit(int[] gas, int[] cost) {
        int res = 0;
        
        int sGas = 0, sCost = 0, total = 0;
        
        // 각 총합을 구한다.
        for (int i = 0; i < gas.length; i++) {
            sGas += gas[i];
            sCost += cost[i];
        }
        
        // 비용의 합이 가스의 합보다 크면 한 바퀴를 돌 수 없다.
        if (sGas < sCost) return -1;
        
        // 합이 0보다 작아지면 더 이상 진행할 수 없으므로 시작 지점을 옮겨야 한다.
        for (int i = 0; i < gas.length; i++) {
            total += gas[i] - cost[i];
            if (total < 0) {
                total = 0;
                res = i + 1;
            }
        }
        
        return res;
    }
}
```
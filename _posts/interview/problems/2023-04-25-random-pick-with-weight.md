---
layout: post
published: true
title: "528. Random Pick with Weight"
categories: interview
tags: problems array binary-search prefix-sum
---

> [0, w.length - 1] 범위의 인덱스를 임의로 선택하여 반환하는 pickIndex() 함수를 구현
> - 인덱스 i를 선택할 확률은 w[i] / sum(w)

- [528. Random Pick with Weight](https://leetcode.com/problems/random-pick-with-weight/)

```java
class Solution {

    Random random;
    
    // 가중치의 합
    int[] wSums;
    
    // w: 가중치 배열
    public Solution(int[] w) {
        this.random = new Random();
        
        for (int i = 1; i < w.length; ++i) {
            w[i] += w[i-1];
        }
        
        this.wSums = w;
        
        //Arrays.parallelPrefix(wSums, Integer::sum);
    }
    
    public int pickIndex() {
        int nextInt = random.nextInt(wSums[wSums.length - 1]);
        int i = Arrays.binarySearch(wSums, nextInt);
        return Math.abs(i + 1);
    }
}

/**
 * Your Solution object will be instantiated and called as such:
 * Solution obj = new Solution(w);
 * int param_1 = obj.pickIndex();
 */
```
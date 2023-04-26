---
layout: post
published: true
title: "528. Random Pick with Weight"
categories: interview
tags: problems array binary-search prefix-sum
---

> 큰 정수를 1씩 증가시키고 결과 숫자 배열을 반환

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
---
layout: post
published: true
title: "384. Shuffle an Array"
categories: interview
tags: medium math
---

> 정수 배열 숫자가 주어지면 배열을 무작위로 섞는 알고리즘을 설계  

[384. Shuffle an Array](https://leetcode.com/problems/shuffle-an-array/)

```java
class Solution {

    private Random random = new Random();

    // 원본 배열
    private int[] nums;

    public Solution(int[] nums) {
        this.nums = nums;
    }
    
    /** Resets the array to its original configuration and return it. */
    public int[] reset() {
        return nums;
    }
    
    /** Returns a random shuffling of the array. */
    // Fisher-Yates algorithm: 수열의 무작위 순열을 생성하기 위한 알고리즘
    // O(n), O(1)
    public int[] shuffle() {
        int[] a = nums.clone();
        
        // 뒤에서 부터 무작위 위치로 스왑한다.
        for (int lastIndex = a.length - 1; lastIndex > 0; lastIndex--) {
            int rendIndex = random.nextInt(lastIndex + 1);
            swap(a, rendIndex, lastIndex);
        }
        
        return a;
    }
    
    private void swap(int[] a, int i, int j) {
        int t = a[i];
        a[i] = a[j];
        a[j] = t;
    }
}

/**
 * Your Solution object will be instantiated and called as such:
 * Solution obj = new Solution(nums);
 * int[] param_1 = obj.reset();
 * int[] param_2 = obj.shuffle();
 */
```
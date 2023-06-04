---
layout: post
published: true
title: "72. Edit Distance"
categories: interview
tags: string dynamic-programming
---

> word1을 word2로 변환하는 데 필요한 최소 작업 수

- [72. Edit Distance](https://leetcode.com/problems/edit-distance/)


```java
class Solution {

    String word1, word2;
    int[][] dp;

    // word1을 word2로 변환하는 데 필요한 최소 작업 수
    public int minDistance(String word1, String word2) {
        this.word1 = word1;
        this.word2 = word2;

        int m = word1.length() - 1;
        int n = word2.length() - 1;
        
        dp = new int[m + 2][n + 2];

        for (int[] d : dp) {
            Arrays.fill(d, -1);
        }
        
        return helper(m, n);
    }

    public int helper(int m, int n) {
        //the strings are null
        if (m + 1 == 0 && n + 1 == 0) {
            return 0;
        }
        
        //one of the strings are null
        if (m + 1 == 0 || n + 1 == 0) {
            return Math.max(m + 1, n + 1);
        }
        
        //both values at the index are equal
        if (dp[m][n] != -1) return dp[m][n];
        
        if (word1.charAt(m) == word2.charAt(n)) {
            dp[m][n] = helper(m - 1, n - 1);

            return dp[m][n];
        } else {
            int del = 1 + helper(m - 1, n);     //try deletion
            int ins = 1 + helper(m, n - 1);     //try insertion
            int rep = 1 + helper(m - 1, n - 1); //try replacing

            //now we'll choose the minimum out of these 3 and add 1 for the operation cost
            dp[m][n] = Math.min(Math.min(del, ins), rep);

            return dp[m][n];
        }
    }
}

```

---
layout: post
published: true
title: "97. Interleaving String"
categories: interview
tags: problems dynamic-programming string
---

> 문자열 s1, s2 및 s3이 주어지면 s3이 s1 및 s2의 인터리빙에 의해 형성되는지 확인
> An interleaving of two strings s and t is a configuration where s and t are divided into n and m substrings respectively, such that:

![](https://assets.leetcode.com/uploads/2020/09/02/interleave.jpg)

- [97. Interleaving String](https://leetcode.com/problems/interleaving-string/)

```java
class Solution {
    
    // 문자열 s1, s2 및 s3이 주어지면 s3이 s1 및 s2의 인터리빙에 의해 형성되는지 확인
    // T: O(nm)
    public boolean isInterleave(String s1, String s2, String s3) {
        if (s1.length() + s2.length() != s3.length()) {
            return false;
        }

        boolean[][] dp = new boolean[s1.length() + 1][s2.length() + 1];
        dp[s1.length()][s2.length()] = true;

        for (int i = dp.length - 1; i >= 0; i--) {
            for (int j = dp[0].length - 1; j >= 0; j--) {
                if (i < s1.length() && s1.charAt(i) == s3.charAt(i + j) && dp[i + 1][j]) {
                    dp[i][j] = true;
                }
                
                if (j < s2.length() && s2.charAt(j) == s3.charAt(i + j) && dp[i][j + 1]) {
                    dp[i][j] = true;
                }
            }
        } 

        return dp[0][0];
    }
}
```
---
layout: post
published: true
title: "1143. Longest Common Subsequence"
categories: interview
tags: medium string dynamic-programming
---

> 두 개의 문자열 text1과 text2가 주어지면 가장 긴 공통 하위 시퀀스의 길이를 반환   
> 공통 하위 시퀀스가 ​​없으면 0을 반환

[1143. Longest Common Subsequence](https://leetcode.com/problems/longest-common-subsequence/)

상향식 2차원 동적 프로그래밍 방식으로 서브스트링을 비교하는 서브문제로 나누어서 해결한다.

```java
class Solution {

    // 두 문자열의 가장 긴 부분 문자열의 길이
    // Dynamic Programming : 서브 문제로 나눌 수 있으면 
    // Bottom-up: O (n * m)
    public int longestCommonSubsequence(String text1, String text2) {
        int l1 = text1.length();
        int l2 = text2.length();
        
        // 공백 문자일 때를 기본값(0) 으로 시작한다.
        int dp[][] = new int[l1 + 1][l2 + 1];
		
        for (int i = l1 - 1; i >= 0; i--) {
            for (int j = l2 - 1; j >= 0; j--) {
                //if two characters match, length of the common subsequence would be 1 plus the length of the common subsequence till the 0 indexes
                if (text1.charAt(i) == text2.charAt(j))  {
                    dp[i][j] = 1 + dp[i+1][j+1];
                } 
                //if two characters doesn't match, we will take the longer by either skipping i or j indexes
                else  { 
                    dp[i][j] = Math.max(dp[i][j+1], dp[i+1][j]);
                }
            }
        }
        
        return dp[0][0];
    }
}
```

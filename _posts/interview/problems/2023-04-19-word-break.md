---
layout: post
published: true
title: "139. Word Break"
categories: interview
tags: string dynamic-programming
---

> s가 공백으로 구분된 하나 이상의 사전 단어 시퀀스로 분할될 수 있는 경우 true를 반환

- [139. Word Break](https://leetcode.com/problems/word-break/)

```java
class Solution {
    
    // O(n * m * n)
    // Decision Tree -> Cache -> DP
    public boolean wordBreak(String s, List<String> wordDict) {
		int length = s.length();

		// dp[i] represents whether s[0...i] can be formed by dict
		boolean[] dp = new boolean[length + 1];
        
        // for bottom-up base case
        dp[length] = true;

		for (int i = length - 1; i >= 0 ; i--) {
			for (String word: wordDict) {
				int wl = word.length(); // 단어길이 만큼씩 처리한다.
				if (i + wl <= length && s.substring(i, i + wl).startsWith(word)) {
                    // 점화식: 상향식 접근법으로 뒤에서 부터 서브문제로 처리
					dp[i] = dp[i + wl];
				}
            
                // 단어가 존재하면 다음 인덱스로 넘어간다.
                if (dp[i]) {
                    break;
                }
			}
		}

		return dp[0];
	}
}
```
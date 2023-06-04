---
layout: post
published: true
title: "22. Generate Parentheses"
categories: interview
tags: backtracking
---

> n 쌍의 괄호가 주어지면 올바른 형식의 괄호 조합을 모두 생성하는 함수를 작성

- [22. Generate Parentheses](https://leetcode.com/problems/generate-parentheses/)

```java
class Solution {
    List<String> ans = new ArrayList();
    StringBuilder cur = new StringBuilder();
    
    // 괄호의 모든 조합
    public List<String> generateParenthesis(int n) {
        backtrack(0, 0, n);
         
        return ans;
    }

    public void backtrack(int open, int close, int n) {
        // 종료조건(open == close)
        if (cur.length() == n * 2) {
            ans.add(cur.toString());
            return;
        }

        // only add open parenthesis if open < n
        if (open < n) {
            cur.append("(");
            backtrack(open + 1, close, n);
            cur.deleteCharAt(cur.length() - 1);  // 가장 마지막 문자를 지운다.
        }
        
        // only add a closing paranthesis if close < open
        if (close < open) {
            cur.append(")");
            backtrack(open, close + 1, n);
            cur.deleteCharAt(cur.length() - 1);
        }
    }
}
```
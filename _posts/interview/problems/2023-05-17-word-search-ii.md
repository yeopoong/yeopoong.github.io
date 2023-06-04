---
layout: post
published: true
title: "212. Word Search II"
categories: interview
tags: backtracking matrix
---

> m x n 문자 보드와 문자열 단어 목록이 주어지면 보드의 모든 단어를 반환

- [212. Word Search II](https://leetcode.com/problems/word-search-ii/)

![](https://assets.leetcode.com/uploads/2020/11/07/search1.jpg)

```java
class Solution {
    
    List<String> res = new ArrayList<>();
    
    public List<String> findWords(char[][] board, String[] words) {
        TrieNode root = buildTrie(words);
        
        for (int i = 0; i < board.length; i++) {
            for (int j = 0; j < board[0].length; j++) {
                dfs(board, i, j, root);
            }
        }
        
        return res;
    }

    public void dfs(char[][] board, int i, int j, TrieNode p) {
        char c = board[i][j];
        
        if (c == '#' || p.next[c - 'a'] == null) return;
        
        p = p.next[c - 'a'];
        if (p.word != null) {   // found one
            res.add(p.word);
            p.word = null;     // de-duplicate
        }

        board[i][j] = '#';
        
        if (i > 0) dfs(board, i - 1, j ,p); 
        if (j > 0) dfs(board, i, j - 1, p);
        if (i < board.length - 1) dfs(board, i + 1, j, p); 
        if (j < board[0].length - 1) dfs(board, i, j + 1, p); 
        
        board[i][j] = c;
    }

    public TrieNode buildTrie(String[] words) {
        TrieNode root = new TrieNode();
        
        for (String w : words) {
            TrieNode p = root;
            for (char c : w.toCharArray()) {
                int i = c - 'a';
                if (p.next[i] == null) p.next[i] = new TrieNode();
                p = p.next[i];
           }
           p.word = w;
        }
        
        return root;
    }

    class TrieNode {
        String word;
        TrieNode[] next = new TrieNode[26];
    }
}
```
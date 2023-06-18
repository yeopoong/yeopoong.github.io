---
layout: post
published: true
title: "211. Design Add and Search Words Data Structure"
categories: interview
tags: medium design
---

> 새 단어 추가를 지원하고 문자열이 이전에 추가된 문자열과 일치하는지 확인하는 데이터 구조를 설계  
> - void addWord(word) 데이터 구조에 단어를 추가하고 나중에 일치시킬 수 있습니다.  
> - bool search(word) 데이터 구조에 단어와 일치하는 문자열이 있으면 true를 반환하고 그렇지 않으면 false를 반환

[211. Design Add and Search Words Data Structure](https://leetcode.com/problems/design-add-and-search-words-data-structure/)

```java
class WordDictionary {
    
    Node root;

    public WordDictionary() {
        root = new Node('\0');
    }

    public void addWord(String word) {
        Node curr = root;

        for (int i = 0; i < word.length(); i++) {
            char ch = word.charAt(i);

            if (curr.children[ch - 'a'] == null) {
                curr.children[ch - 'a'] = new Node(ch);
            }

            curr = curr.children[ch - 'a'];
        }

        curr.isWord = true;
    }

    // TC O(m^2)
    public boolean search(String word) {
        return searchHelper(word, root, 0);
    }

    private boolean searchHelper(String word, Node curr, int index) {
        for (int i = index; i < word.length(); i++) {
            char ch = word.charAt(i);

            if (ch == '.') {
                for (Node temp : curr.children) {
                    if (temp != null && searchHelper(word, temp, i + 1)) {
                        return true;
                    }
                }

                return false;
            }

            if (curr.children[ch - 'a'] == null) {
                return false;
            }

            curr = curr.children[ch - 'a'];
        }

        return curr.isWord;
    }
    
    private class Node {
        char value;
        boolean isWord;
        Node[] children;

        public Node(char value) {
            this.value = value;
            isWord = false;
            children = new Node[26];
        }
    }
}

/**
 * Your WordDictionary object will be instantiated and called as such:
 * WordDictionary obj = new WordDictionary();
 * obj.addWord(word);
 * boolean param_2 = obj.search(word);
 */
```

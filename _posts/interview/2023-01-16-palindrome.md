---
layout: post
published: false
title: "Palindrome"
categories: interview
tags: topics palindrome
---

## Palindrome

> A phrase is a palindrome if, after converting all uppercase letters into lowercase letters and removing all non-alphanumeric characters, it reads the same forward and backward. Alphanumeric characters include letters and numbers.

- 중복되지 않는 문자는 중간에 한번만 나올 수 있다.
- 센터에서 확장하면서 처리한다.

Two Pointers
```java
 public boolean isPalindrome(String s) {
    int i = 0, j = s.length() - 1;
    
    while (i < j) {
        if (s.charAt(i) == s.charAt(j)) {
            i++; 
            j--;
        } else {
            return false;
        }
    }
    
    return true;
}
```

```java
String result;
int maxLen;

public void getPalindrome(String s, int left, int right) {
    int len = 0;
    
    // 팰린드롬이면 길이를 넓혀서 체크한다(인바운드와 팰린드롬 체크)
    while (left >= 0 && right < s.length() && s.charAt(left) == s.charAt(right)) {
        len = right - left + 1;
        // 현재길이가 최대길이보다 크면 결과 문자열을 업데이트 한다.
        if (len > maxLen) {
            result = s.substring(left, right + 1);
            maxLen = len;
        }
        left--;
        right++;
    }
}
```

[Easy]
- [125. Valid Palindrome](/interview/2023/02/20/valid-palindrome/)
- [409. Longest Palindrome](/interview/2023/04/09/longest-palindrome/)
- [9. Palindrome Number](/interview/2023/05/21/palindrome-number/)

[Medium]
- [647. Palindromic Substrings](/interview/2023/05/21/palindromic-substrings/)
- [5. Longest Palindromic Substring](/interview/2023/05/21/longest-palindromic-substring)
- [131. Palindrome Partitioning](/interview/2023/05/21/palindrome-partitioning/)
- [214. Shortest Palindrome](/interview/2023/05/21/shortest-palindrome/)
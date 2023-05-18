---
layout: post
published: true
title: "17. Letter Combinations of a Phone Number"
categories: interview
tags: problems backtracking
---

> 전화번호의 숫자가 나타낼 수 있는 가능한 모든 문자 조합을 반환

- [17. Letter Combinations of a Phone Number](https://leetcode.com/problems/letter-combinations-of-a-phone-number/)

![](https://assets.leetcode.com/uploads/2022/03/15/1200px-telephone-keypad2svg.png)

```java
class Solution {
    private static final String[] KEYS = { "", "", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz" };
    
    List<String> result = new ArrayList<>();
    
    // 전화번호의 숫자가 나타낼 수 있는 가능한 모든 문자 조합을 반환 
    // T: O(n*4^n), where n is the length of digits 
    // S: O(n)
    public List<String> letterCombinations(String digits) {
        
        if (digits.length() > 0) {
            backtrack(0, "", digits);
        }
        
        return result;
    }

    // 함수 호출 시에 문자열 복사가 발생하므로 문자열의 길이 만큼 시간복잡도가 필요하다.
    // index: 숫자문자열의 인덱스
    // letter: 문자열 조합
    private void backtrack(int index, String letter, String digits) {
        // 마지막 숫자까지 처리했으면 결과에 추가한다.
        if (index == digits.length()) {
            result.add(letter);
            return;
        }
        
        // 숫자가 표시하는 문자열
        String letters = KEYS[(digits.charAt(index) - '0')];
        
        // 문자열의 조합을 구한다.
        for (int i = 0; i < letters.length(); i++) {
            backtrack(index + 1, letter + letters.charAt(i), digits);
        }
    }
}
```
---
layout: post
published: true
title: "345. Reverse Vowels of a String"
categories: interview
tags: string two-pointers
---

> 문자열 s가 주어지면 문자열의 모든 모음만 반전시켜 반환

- [345. Reverse Vowels of a String](https://leetcode.com/problems/reverse-vowels-of-a-string/)

```java
class Solution {
    public String reverseVowels(String s) {
        Set<Character> set = new HashSet<>(Arrays.asList('a', 'e', 'i', 'o', 'u', 'A', 'E', 'I', 'O', 'U'));
        
        char[] arr = s.toCharArray();
        int left = 0, right = arr.length - 1;
        
        while (left < right) {
            // 왼쪽 모음을 체크한다. 
            if (!set.contains(arr[left])) {
                left++;
            // 오른쪽 모음을 체크한다.
            } else if (!set.contains(arr[right])) {
                right--;
            // 양쪽 모두 모음이면 스왑한다.
            } else {
                swap(arr, left++, right--);
            }
        }
        
        return new String(arr);   
    }
    
    public void swap(char[] s, int left, int right) {
        char temp;
        temp = s[right];
        s[right] = s[left];
        s[left] = temp; 
    }
}
```
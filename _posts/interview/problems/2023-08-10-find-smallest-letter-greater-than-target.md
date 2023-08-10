---
layout: post
published: true
title: "744. Find Smallest Letter Greater Than Target"
categories: interview
tags: easy binary-search 
---

> 감소하지 않는 순서로 정렬된 문자 배열에서 사전순으로 target보다 큰 문자 중 가장 작은 문자를 반환합니다. 해당 문자가 없으면 문자의 첫 번째 문자를 반환

[744. Find Smallest Letter Greater Than Target](https://leetcode.com/problems/find-smallest-letter-greater-than-target/)

```java
class Solution {
    
    // T: O(logn)
    public char nextGreatestLetter(char[] letters, char target) {
        int left = 0, right = letters.length - 1, mid;
        
        while (left <= right) {
            mid = (left + right) / 2;
            if (letters[mid] <= target) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }

        return left == letters.length ? letters[0] : letters[left];
    }
}
```
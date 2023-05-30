---
layout: post
published: true
title: "340. Longest Substring with At Most K Distinct Characters"
categories: interview
tags: problems string sliding-window hashmap
---

> 문자열 s와 정수 k가 주어지면 최대 k개의 개별 문자를 포함하는 s의 가장 긴 하위 문자열의 길이를 반환

- [340. Longest Substring with At Most K Distinct Characters](https://leetcode.com/problems/longest-substring-with-at-most-k-distinct-characters/)

```java
class Solution {
    
    // 최대 K 고유 문자가 있는 가장 긴 하위 문자열
    // T: O(n)
    public int lengthOfLongestSubstringKDistinct(String s, int k) {
        int maxLength = 1;
        
        if (k == 0) {
            return 0;
        }
        
        Map<Character, Integer> map = new HashMap<>();

        int left = 0, right = 0;
        while (right < s.length()) {
            map.put(s.charAt(right), right);

            if (map.size() > k) {
                left = Collections.min(map.values());
                map.remove(s.charAt(left));
                left++;
            }

            maxLength = Math.max(maxLength, right - left + 1);
            right++;
        }
        
        return maxLength;
    }
}
```
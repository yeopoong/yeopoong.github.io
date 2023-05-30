---
layout: post
published: true
title: "159. Longest Substring with At Most Two Distinct Characters"
categories: interview
tags: problems string sliding-window hashmap
---

> 문자열 s가 주어지면 최대 2개의 개별 문자를 포함하는 가장 긴 하위 문자열의 길이를 반환

- [159. Longest Substring with At Most Two Distinct Characters](https://leetcode.com/problems/longest-substring-with-at-most-two-distinct-characters/)

```java
class Solution {
    
    // 최대 두 개의 개별 문자를 포함하는 가장 긴 하위 문자열의 길이
    // T: O(n)
    public int lengthOfLongestSubstringTwoDistinct(String s) {
        int longest = 1;
        
        // sliding window left and right pointers
        int left = 0, right = 0;
        
        // 문자와 인덱스를 저장한다.
        HashMap<Character, Integer> map = new HashMap<>();

        while (right < s.length()) {
            // 문자를 맵에 넣는다. 
            map.put(s.charAt(right), right);

            // 맵에 문자가 3개가 되면 가장 왼쪽 문자를 지운다. 
            if (map.size() == 3) {
                // 값중에서 최소값을 찾는다. 
                left = Collections.min(map.values());
                // 해당 위치의 문자를 맵에서 지운다.
                map.remove(s.charAt(left));
                left += 1;
            }

            longest = Math.max(longest, right - left + 1);
            right++;
        }
        
        return longest;
    }
}
```
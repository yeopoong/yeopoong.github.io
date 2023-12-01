---
layout: post
published: true
title: "3. Longest Substring Without Repeating Characters"
categories: interview
tags: string sliding-window hashmap longest
---

> 문자열 s가 주어지면 반복되는 문자가 없는 가장 긴 하위 문자열의 길이를 구하라.

[3. Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)

```java
class Solution {
    // 반복되는 문자가 없는 가장 긴 하위 문자열
    // Sliding Window with Two Pointer
    // O(n): the contains() of HashSet runs in O(1) time. Getting the object's bucket location is a constant time operation. 
    // Taking into account possible collisions, the lookup time may rise to log(n) because the internal bucket structure is a TreeMap.
    // This is an improvement from Java 7 which used a LinkedList for the internal bucket structure. 
    // In general, hash code collisions are rare. So we can consider the elements lookup complexity as O(1).
    public int lengthOfLongestSubstring(String s) {
        int max = 0;
        
        // Two Pointer
        int start = 0, end = 0;
        
        // 중복 체크를 위한 저장소(반복 되지 않는 문자만 저장한다)
        Set<Character> set = new HashSet<>();

        while (end < s.length()) {
            // 중복체크
            if (!set.contains(s.charAt(end))) {
                // 처음 나온 문자면 저장하고 종료위치 증가
                set.add(s.charAt(end++));
                // 최대 문자열 길이 갱신(윈도우 크기가 줄어들수도 있기 때문에 최대값을 계속 갱신해야 한다)
                max = Math.max(max, set.size());
            } else {
                // 이미 나온 문자면 저장소에서 해당 문자 삭제하고 시작 위치 갱신 (종료 위치는 그대로 다음에 또 체크)
                // : 서브스트링을 구해야 하기 때문에 시작 윈도우 값을 증가하면서 중복된 문자를 찾는다.
                set.remove(s.charAt(start++));
            }
        }

        return max;
    }
}
```
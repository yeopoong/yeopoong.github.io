---
layout: post
published: true
title: "2405. Optimal Partition of String"
categories: interview
tags: medium string
---

> 각 하위 문자열의 문자가 고유하도록 문자열을 하나 이상의 하위 문자열로 분할할 수 있는 하위 문자열의 최소 수를 반환

[2405. Optimal Partition of String](https://leetcode.com/problems/optimal-partition-of-string/)

```java
class Solution {
    
    // 문자열의 최적 분할
    // T: O(n)
    public int partitionString(String s) {
        int count = 1, substringStart = 0;
        
        int[] lastSeen = new int[26];
        Arrays.fill(lastSeen, -1);

        for (int i = 0; i < s.length(); i++) {
            // 동일한 문자가 이미 서브스트링에 존재하면 새로운 서브스트링을 만든다. 
            if (lastSeen[s.charAt(i) - 'a'] >= substringStart) {
                count++;
                substringStart = i;
            }
            lastSeen[s.charAt(i) - 'a'] = i;
        }

        return count;
    }
}
```
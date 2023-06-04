---
layout: post
published: true
title: "451. Sort Characters By Frequency"
categories: interview
tags: string hashmap heap
---

> 문자열 s가 주어지면 문자 빈도에 따라 내림차순으로 정렬

- [451. Sort Characters By Frequency](https://leetcode.com/problems/sort-characters-by-frequency/)

```java
class Solution {
    
    // 빈도로 문자 정렬(빈도를 계산하고 우선순위로 문자를 정렬)
    // O(nlogm)
    public String frequencySort(String s) {
        Map<Character, Integer> map = new HashMap<>();
        
        // 문자별로 카운트한다.
        for (char c : s.toCharArray()) {
            map.put(c, map.getOrDefault(c, 0) + 1);
        }
						
        // 우선순위 큐에 빈도순으로 키값을 넣는다.
        PriorityQueue<Character> pq = new PriorityQueue<>((a, b) -> map.get(b) - map.get(a));
        pq.addAll(map.keySet());
				
        StringBuilder sb = new StringBuilder();
        while (!pq.isEmpty()) {
            char c = pq.poll();
            // 해당 문자의 빈도만큼 문자열을 추가한다.
            for (int i = 0; i < (int) map.get(c); i++) {
                sb.append(c);
            }
        }
        
        return sb.toString();
    }
}
```

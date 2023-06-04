---
layout: post
published: true
title: "692. Top K Frequent Words"
categories: interview
tags: heap hashamp
---

> 문자열 단어의 배열과 정수 k가 주어지면 가장 자주 사용되는 k개의 문자열을 반환

- [692. Top K Frequent Words](https://leetcode.com/problems/top-k-frequent-words/)

```java
class Solution {
    public List<String> topKFrequent(String[] words, int k) {
        Map<String, Integer> map = new HashMap<>();
        
        for (String word : words) {
            map.put(word, map.getOrDefault(word, 1) + 1);
        }
        
        PriorityQueue<String> pq = new PriorityQueue<>(
            (a, b) -> map.get(a) == map.get(b) ? a.compareTo(b) : map.get(b) - map.get(a)
        );
        
        for (String key : map.keySet()) {
            pq.offer(key);
        }

        List<String> result = new LinkedList<>();
        
        for (int i = 0; i < k; i++) {
            result.add(pq.poll());
        }
        
        return result;
    }
}
```
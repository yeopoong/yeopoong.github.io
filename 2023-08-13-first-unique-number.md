---
layout: post
published: true
title: "1429. First Unique Number"
categories: interview
tags: medium queue design
---

> 정수 큐가 있고 큐에서 첫 번째 고유 정수를 검색

[1429. First Unique Number](https://leetcode.com/problems/first-unique-number/)

```java
class FirstUnique {

    Map<Integer, Integer> freq = new HashMap<>();
    Queue<Integer> q = new LinkedList<>();
    
    // T: O(n)
    public FirstUnique(int[] nums) {
        for (int x : nums) {
            add(x);
        }
    }
    
    // T: O(n)
    public int showFirstUnique() {
        while (!q.isEmpty() && freq.get(q.peek()) > 1) {
            q.poll();
        }
        
        return q.isEmpty() ? -1 : q.peek();
    }
    
    // T: O(1)
    public void add(int value) {
        freq.put(value, freq.getOrDefault(value, 0) + 1);
        q.offer(value);
    }
}

/**
 * Your FirstUnique object will be instantiated and called as such:
 * FirstUnique obj = new FirstUnique(nums);
 * int param_1 = obj.showFirstUnique();
 * obj.add(value);
 */
```
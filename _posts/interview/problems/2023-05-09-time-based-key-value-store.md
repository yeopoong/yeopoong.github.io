---
layout: post
published: true
title: "981. Time Based Key-Value Store"
categories: interview
tags: array hashmap
---

> 서로 다른 타임스탬프에서 동일한 키에 대한 여러 값을 저장하고 특정 타임스탬프에서 키 값을 검색할 수 있는 시간 기반 키-값 데이터 구조를 설계  

- [981. Time Based Key-Value Store](https://leetcode.com/problems/time-based-key-value-store/)

![](https://leetcode.com/problems/time-based-key-value-store/Figures/981/slides/Slide1.png)

Sorted Map + Binary Search
```java
class TimeMap {

    HashMap<String, TreeMap<Integer, String>> map;

    // 서로 다른 타임스탬프에서 동일한 키에 대한 여러 값을 저장하고 
    // 특정 타임스탬프에서 키 값을 검색할 수 있는 시간 기반 키-값 데이터 구조를 설계
    public TimeMap() {
        map = new HashMap<>();
    }
    
    // T: O(logn)
    public void set(String key, String value, int timestamp) {
        if (!map.containsKey(key)) {
            map.put(key, new TreeMap<Integer, String>());
        }
        
        map.get(key).put(timestamp, value);
    }
    
    // T: O(logn)
    public String get(String key, int timestamp) {
        if (!map.containsKey(key)) {
            return "";
        }
        
        // timestamp보다 작은 가장 최근 데이터를 찾는다.
        Integer floorKey = map.get(key).floorKey(timestamp);
        if (floorKey != null) {
            return map.get(key).get(floorKey);
        }
        
        return "";
    }
}

/**
 * Your TimeMap object will be instantiated and called as such:
 * TimeMap obj = new TimeMap();
 * obj.set(key,value,timestamp);
 * String param_2 = obj.get(key,timestamp);
 */
```

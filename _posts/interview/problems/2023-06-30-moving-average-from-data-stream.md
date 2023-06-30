---
layout: post
published: true
title: "346. Moving Average from Data Stream"
categories: interview
tags: easy design
---

> 정수 스트림과 윈도우 크기가 주어지면 슬라이딩 윈도우에 있는 모든 정수의 이동 평균을 계산

[346. Moving Average from Data Stream](https://leetcode.com/problems/rotting-oranges/)

```java
class MovingAverage {

    int size;
    List<Integer> queue = new ArrayList<>();
    
    public MovingAverage(int size) {
        this.size = size;
    }
    
    // 스트림의 마지막 크기 값의 이동 평균을 반환
    // T: O(n)
    public double next(int val) {
        queue.add(val);
        
        // calculate the sum of the moving window
        int windowSum = 0;
        for (int i = Math.max(0, queue.size() - size); i < queue.size(); ++i) {
            windowSum += queue.get(i);
        }

        return windowSum * 1.0 / Math.min(queue.size(), size);
    }
}

/**
 * Your MovingAverage object will be instantiated and called as such:
 * MovingAverage obj = new MovingAverage(size);
 * double param_1 = obj.next(val);
 */
```
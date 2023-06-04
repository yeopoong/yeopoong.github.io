---
layout: post
published: true
title: "295. Find Median from Data Stream"
categories: interview
tags: design heap
---

> MedianFinder 클래스를 구현
> - void addNum(int num): 데이터 스트림의 정수값을 데이터 구조에 추가
> - double findMedian(): 모든 요소의 중앙값을 반환

- [295. Find Median from Data Stream](https://leetcode.com/problems/find-median-from-data-stream/)

```java
class MedianFinder {

    // two heap
    private Queue<Integer> smallHeap; //small elements - maxHeap
    private Queue<Integer> largeHeap; //large elements - minHeap

    public MedianFinder() {
        smallHeap = new PriorityQueue<>((a, b) -> b - a);
        largeHeap = new PriorityQueue<>((a, b) -> a - b);
    }

    // O(log n)
    public void addNum(int num) {
        smallHeap.add(num);

        // make sure every num small is <= every num in large
        if (!largeHeap.isEmpty() && smallHeap.peek() > largeHeap.peek() ) {
            largeHeap.add(smallHeap.poll());
        }

        // uneven size?
        if (largeHeap.size() - smallHeap.size() > 1) {
            smallHeap.add(largeHeap.poll());
        } else if (smallHeap.size() - largeHeap.size() > 1) {
            largeHeap.add(smallHeap.poll());
        }
    }

    // O(1)
    public double findMedian() {
        if (smallHeap.size() > largeHeap.size()) {
            return (double) smallHeap.peek();
        } else if (smallHeap.size() < largeHeap.size()) {
            return (double) largeHeap.peek();
        } else {
            return (double) (largeHeap.peek() + smallHeap.peek()) / 2;
        }
    }
}

/**
 * Your MedianFinder object will be instantiated and called as such:
 * MedianFinder obj = new MedianFinder();
 * obj.addNum(num);
 * double param_2 = obj.findMedian();
 */
```

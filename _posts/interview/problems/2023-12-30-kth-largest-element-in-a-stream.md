---
layout: post
published: true
title: "703. Kth Largest Element in a Stream"
categories: interview
tags: easy heaps
---

> 스트림에서 k번째로 큰 요소를 찾는 클래스를 설계

[703. Kth Largest Element in a Stream](https://leetcode.com/problems/kth-largest-element-in-a-stream/)

```java
class KthLargest {

    private static int k;
    private PriorityQueue<Integer> heap;
    
    public KthLargest(int k, int[] nums) {
        this.k = k;
        heap = new PriorityQueue<>();
        
        for (int num: nums) {
            heap.offer(num);
        }
        
        while (heap.size() > k) {
            heap.poll();
        }
    }
    
    public int add(int val) {
        heap.offer(val);
        
        if (heap.size() > k) {
            heap.poll();
        }
        
        //System.out.println(heap);

        return heap.peek();
    }
}

```
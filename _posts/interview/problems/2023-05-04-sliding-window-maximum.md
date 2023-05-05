---
layout: post
published: true
title: "239. Sliding Window Maximum"
categories: interview
tags: problems array sliding-window queue
---

> 사이즈 K인 슬라이딩 윈도우의 최대값 리스트

- [239. Sliding Window Maximum](https://leetcode.com/problems/sliding-window-maximum/)


```java
class Solution {

    // 사이즈 K인 슬라이딩 윈도우의 최대값 리스트
    // Brute force: O(k*(n-k))
    // Sliding Window: O(n)
    public int[] maxSlidingWindow(int[] nums, int k) {
        int[] ans = new int[nums.length - k + 1];

        int w = 0; // 윈도우 그룹의 인덱스
        
        // Monotonically Decreasing Queue
        Deque<Integer> deque = new LinkedList<>();
        
        for (int i = 0; i < nums.length; i++) {
            // 큐에 추가된 값이 윈도우 범위보다 크면 첫번째 값을 제거
            if (!deque.isEmpty() && deque.peekFirst() < i + 1 - k) {
                deque.pollFirst();
            }

            // * 큐에서 추가될 값보다 작은값들을 제거
            while (!deque.isEmpty() && nums[i] > nums[deque.peekLast()]) {
                deque.pollLast();
            }

            // * 큐에 새로운 값 추가
            deque.offer(i);

            // 윈도우 크기가 K보다 크면 최대값을 결과 리스트에 저장한다.
            if (i + 1 >= k) {
                ans[w++] = nums[deque.peekFirst()];
            }
        }

        return ans;
    }
}
```

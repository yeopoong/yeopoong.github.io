---
layout: post
published: true
title: "933. Number of Recent Calls"
categories: interview
tags: design queue
---

> 특정 시간 프레임 내의 최근 요청 수를 계산하는 RecentCounter 클래스 구현

- [933. Number of Recent Calls](https://leetcode.com/problems/number-of-recent-calls/)

```java
class RecentCounter {

    LinkedList<Integer> slideWindow;

    // 최근 통화 수
    public RecentCounter() {
        this.slideWindow = new LinkedList<Integer>();
    }

    // T: O(1)
    public int ping(int t) {
        // step 1). append the current call
        slideWindow.addLast(t);

        // step 2). invalidate the outdated pings
        while (slideWindow.getFirst() < t - 3000) {
            slideWindow.removeFirst();
        }

        return slideWindow.size();
    }
}

/**
 * Your RecentCounter object will be instantiated and called as such:
 * RecentCounter obj = new RecentCounter();
 * int param_1 = obj.ping(t);
 */
```
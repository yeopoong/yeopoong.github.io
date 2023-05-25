---
layout: post
published: true
title: "1823. Find the Winner of the Circular Game"
categories: interview
tags: problems queue simulation
---

> 친구의 수 n과 정수 k가 주어지면 게임의 승자를 반환

- [1823. Find the Winner of the Circular Game](https://leetcode.com/problems/find-the-winner-of-the-circular-game/)

![](https://assets.leetcode.com/uploads/2021/03/25/ic234-q2-ex11.png)

```java
class Solution {
    // 순환 게임의 승자 찾기
    // n: the number of friends, k: the next k friends
    public int findTheWinner(int n, int k) {
        // 데이터를 순환 시키기 위해서 큐 자료구조를 사용
        Queue<Integer> queue = new LinkedList<>();
        
        // 큐에 모든 숫자를 추가한다.
        for (int i = 1; i <= n; i++) {
            queue.offer(i);
        }
        
        // 마지막 데이터가 남을 때가지 순환하고 지우고를 반복한다.
        while (queue.size() > 1) {
            // K번째를 지우기 위해서 K-1 만큼 순환시킨다.
            int delete = k - 1;
            while (delete-- > 0) {
                // 꺼내서 다시 넣는다.
                queue.offer(queue.remove());
            }
            
            // K번째를 지운다.
            queue.remove();
        }
        
        return queue.peek();
    }
}
```
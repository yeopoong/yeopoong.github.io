---
layout: post
published: true
title: "1584. Min Cost to Connect All Points"
categories: interview
tags: medium union-find graph
---

> 모든 포인트를 연결하기 위한 최소 비용을 반환  
> 두 점 사이에 단순 경로가 정확히 하나만 있으면 모든 점이 연결됨  

[1584. Min Cost to Connect All Points](https://leetcode.com/problems/min-cost-to-connect-all-points/)

manhattan distance = |xi - xj| + |yi - yj|  
![](https://assets.leetcode.com/uploads/2020/08/26/d.png) ![](https://assets.leetcode.com/uploads/2020/08/26/c.png)

```java
class Solution {
        
    // 모든 포인트를 연결하기 위한 최소 비용
    // Time Complexity: O(N^2 log(N)) 
    //  - where N is the length of points. 
    //  - N^2 comes from the fact we need to find the distance between a currNode and every other node to pick the shortest distance. 
    //  - log(N) comes from Priority Queue
    // Space Complexity: O(N^2)
    public int minCostConnectPoints(int[][] points) {
        int cost = 0;
        
        PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> a[0] - b[0]); // edge weight, the index of next node
        pq.offer(new int[] {0, 0});
        
        Set<Integer> visited = new HashSet<>();

        // When visited.size() == points.length meaning that all the nodes has been connected.
        while (visited.size() < points.length) {
            int[] arr = pq.poll();

            int weight = arr[0];
            int currNode = arr[1];

            if (visited.contains(currNode)) continue;

            visited.add(currNode);
            cost += weight;

            for (int nextNode = 0; nextNode < points.length; nextNode++) {
                if (!visited.contains(nextNode)) {
                    int nextWeight = Math.abs(points[nextNode][0] - points[currNode][0]) + Math.abs(points[nextNode][1] - points[currNode][1]);
                    pq.offer(new int[] {nextWeight, nextNode});
                }
            }
        }

        return cost;
    }
}
```

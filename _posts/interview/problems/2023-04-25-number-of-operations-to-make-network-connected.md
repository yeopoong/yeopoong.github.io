---
layout: post
published: true
title: "1319. Number of Operations to Make Network Connected"
categories: interview
tags: problems graph dfs
---

> 모든 네트워크를 연결하기 위한 작업 수: 연결된 그룹의 개수를 카운트 한다.

- [1319. Number of Operations to Make Network Connected](https://leetcode.com/problems/number-of-operations-to-make-network-connected/)

![](https://assets.leetcode.com/uploads/2020/01/02/sample_1_1677.png)

```java
class Solution {
    
    // 네트워크를 연결하기 위한 작업 수
    // n computers: 0 to n - 1
    // T: O(n+m)
    public int makeConnected(int n, int[][] connections) {
        // 연결되지 않은 컴퓨터 그룹의 개수
        int components = 0;
        
        if (connections.length < n - 1) return -1; // To connect all nodes need at least n-1 edges
        
        // 그래프 데이터 생성
        List<Integer>[] graph = new List[n];
        for (int i = 0; i < n; i++) {
            graph[i] = new ArrayList<>();
        }
        
        // 노드별 연결정보
        for (int[] c : connections) {
            graph[c[0]].add(c[1]);
            graph[c[1]].add(c[0]);
        }
        
        boolean[] visited = new boolean[n];
        
        for (int v = 0; v < n; v++) {
            components += dfs(v, graph, visited);
        }
        
        return components - 1; // Need (components-1) cables to connect components together
    }
    
    // 연결된 모든 네크워크를 방문처리 한다.
    int dfs(int c, List<Integer>[] graph, boolean[] visited) {
        if (visited[c]) return 0;
        
        visited[c] = true;
        
        for (int v : graph[c]) {
            dfs(v, graph, visited);
        }
        
        return 1;
    }
}
```
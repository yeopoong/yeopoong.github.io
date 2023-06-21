---
layout: post
published: true
title: "323. Number of Connected Components in an Undirected Graph"
categories: interview
tags: medium graph dfs
---

> 무방향 그래프의 연결된 구성 요소 수를 반환

[323. Number of Connected Components in an Undirected Graph](https://leetcode.com/problems/number-of-connected-components-in-an-undirected-graph/)

![](https://assets.leetcode.com/uploads/2021/03/14/conn1-graph.jpg)

```java
class Solution {
    
    List<Integer>[] adjList;
    
    // 무방향 그래프에서 연결된 컴포넌트의 수를 반환
    // T: O(E + V)
    public int countComponents(int n, int[][] edges) {
        int components = 0;
        
        // 방문여부
        int[] visited = new int[n];
        
        // 노드별 연결 정보를 만들기 위한 리스트를 생성한다.
        adjList = new ArrayList[n]; 
        for (int i = 0; i < n; i++) {
            adjList[i] = new ArrayList<Integer>();
        }
        
        // 무방향 그래프이므로 양방향 정보를 생성한다.
        for (int i = 0; i < edges.length; i++) {
            adjList[edges[i][0]].add(edges[i][1]);
            adjList[edges[i][1]].add(edges[i][0]);
        }
        
        for (int i = 0; i < n; i++) {
            if (visited[i] == 0) {
                dfs(visited, i);
                components++;
            }
        }
        
        return components;
    }
    
    private void dfs(int[] visited, int node) {
        // 방문처리 한다.
        visited[node] = 1;
        
        List<Integer> list = adjList[node];
         
        // 연결된 모든 노드를 탐색한다.
        for (Integer n: list) {
            if (visited[n] == 0) {
                dfs(visited, n);
            }
        }
    }
}
```
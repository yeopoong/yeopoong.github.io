---
layout: post
published: true
title: "547. Number of Provinces"
categories: interview
tags: problems dfs bfs
---

> 연결된 도시 정보가 주어질때 직접 또는 간접적으로 연결된 도시 그룹의 수를 구하기

- [547. Number of Provinces](https://leetcode.com/problems/number-of-provinces/)

```java
class Solution {
    
    // 도시 방문여부
    Set<Integer> visited = new HashSet<>();
    
    // 연결된 도시의 그룹 찾기
    // DFS(Depth First Search)
    // T: O(n^2), S: O(n)
    public int findCircleNum(int[][] isConnected) {
        int count = 0;
        
        // 방문하지 않은 도시를 방문한다.
        for (int i = 0; i < isConnected.length; i++) {
            if (!visited.contains(i)) {
                dfs(isConnected, i);
                count++;
            }
        }
        
        return count;
    }
        
    // 방문하지 않은 연결된 도시를 찾아서 방문처리 한다.
    public void dfs(int[][] isConnected, int i) {
        for (int j = 0; j < isConnected.length; j++) {
            if (isConnected[i][j] == 1 && !visited.contains(j)) {
                visited.add(j);
                dfs(isConnected, j);
            }
        }
    }
}
```
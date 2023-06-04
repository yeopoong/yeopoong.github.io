---
layout: post
published: true
title: "797. All Paths From Source to Target"
categories: interview
tags: graph
---

> 0에서 n - 1까지 레이블이 지정된 n 노드의 방향성 비순환 그래프(DAG)가 주어지면 노드 0에서 노드 n - 1까지 가능한 모든 경로를 찾아 임의의 순서로 반환

- [797. All Paths From Source to Target](https://leetcode.com/problems/all-paths-from-source-to-target/)

![](https://assets.leetcode.com/uploads/2020/09/28/all_1.jpg)

```java
class Solution {
    List<List<Integer>> res = new ArrayList<>();
    List<Integer> path = new ArrayList<>();
    
    // 0부터 n-1까지의 모든 경로 찾기
    public List<List<Integer>> allPathsSourceTarget(int[][] graph) {
        // 0번 노드를 시작노드로 지정
        path.add(0);
        
        // 0번 노드에서 시작
        dfs(graph, 0);
					
        return res;
    }

    private void dfs(int[][] graph, int node) {
        // 마지막 노드에 도달하면 경로를 저장한다.
        if (node == graph.length - 1) {
            res.add(new ArrayList<Integer>(path));
            return;
        }

        // 각 노드에서 연결된 모든 노드를 방문한다.
        for (int next : graph[node]) {
            path.add(next);
            dfs(graph, next);
            path.remove(path.size() - 1);
        }
    }
}
```

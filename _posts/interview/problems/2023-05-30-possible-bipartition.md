---
layout: post
published: true
title: "886. Possible Bipartition"
categories: interview
tags: graph dfs
---

> 모든 사람을 두 그룹으로 나눌 수 있으면 true를 반환

- [886. Possible Bipartition](https://leetcode.com/problems/possible-bipartition/)

```java
class Solution {
    
    // 가능한 이분할
    public boolean possibleBipartition(int n, int[][] dislikes) {        
        List<Integer>[] graph = new List[n + 1];  

        for (int i = 1; i <= n; ++i) {
            graph[i] = new ArrayList<>();        
        }

        for (int[] dislike : dislikes) {
            graph[dislike[0]].add(dislike[1]);
            graph[dislike[1]].add(dislike[0]);
        }

        Integer[] colors = new Integer[n + 1];

        for (int i = 1; i <= n; ++i) {
            // If the connected component that node i belongs to hasn't been colored yet then try coloring it.
            if (colors[i] == null && !dfs(graph, colors, i, 1)) return false;
        }
        
        return true;   
    }

    private boolean dfs(List<Integer>[] graph, Integer[] colors, int currNode, int currColor) {
        colors[currNode] = currColor;

        // Color all uncolored adjacent nodes.
        for (Integer adjacentNode : graph[currNode]) {

            if (colors[adjacentNode] == null) {
                if (!dfs(graph, colors, adjacentNode, currColor * -1)) return false;     

            } else if (colors[adjacentNode] == currColor) {
                return false;                                     
            }
        }
        return true;        
    }
}
```

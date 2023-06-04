---
layout: post
published: true
title: "785. Is Graph Bipartite?"
categories: interview
tags: graph dfs
---

> 모든 사람을 두 그룹으로 나눌 수 있으면 true를 반환

- [785. Is Graph Bipartite?](https://leetcode.com/problems/is-graph-bipartite/)

```java
class Solution {
    
    // 이분할 그래프인지 체크
    // T: O(n + e)
    public boolean isBipartite(int[][] graph) {
        int n = graph.length;
        int[] color = new int[n];
        Arrays.fill(color, -1);

        for (int start = 0; start < n; ++start) {
            if (color[start] == -1) {
                Stack<Integer> stack = new Stack();
                stack.push(start);
                color[start] = 0;

                while (!stack.empty()) {
                    Integer node = stack.pop();
                    for (int nei: graph[node]) {
                        if (color[nei] == -1) {
                            stack.push(nei);
                            color[nei] = color[node] ^ 1;
                        } else if (color[nei] == color[node]) {
                            return false;
                        }
                    }
                }
            }
        }

        return true;
    }
}
```

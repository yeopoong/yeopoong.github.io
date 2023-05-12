---
layout: post
published: true
title: "133. Clone Graph"
categories: interview
tags: problems graph dfs
---

> 그래프의 딥 카피(클론)를 반환

- [133. Clone Graph](https://leetcode.com/problems/clone-graph/)

![](https://assets.leetcode.com/uploads/2019/11/04/133_clone_graph_question.png)

```java
/*
// Definition for a Node.
class Node {
    public int val;
    public List<Node> neighbors;
    public Node() {
        val = 0;
        neighbors = new ArrayList<Node>();
    }
    public Node(int _val) {
        val = _val;
        neighbors = new ArrayList<Node>();
    }
    public Node(int _val, ArrayList<Node> _neighbors) {
        val = _val;
        neighbors = _neighbors;
    }
}
*/

class Solution {

    // * 그래프에서 노드를 중복 생성하지 않기 위해서 사용한다.
    private HashMap<Integer, Node> map = new HashMap<>();

    // Return a deep copy (clone) of the graph.
    // DFS: O(n) = E + V
    public Node cloneGraph(Node node) {
        // 종료조건
        if (node == null) return null;

        // 이미 생성된 노드가 있으면 사용한다.
        Node clone = map.get(node.val);

        if (clone == null) {
            // 노드를 복제하고 맵에 넣는다.
            clone = new Node(node.val);
            map.put(clone.val, clone);
            
            // 원본 노드의 이웃노드를 복제해서 추가한다.
            for (Node neighbor : node.neighbors) {
                clone.neighbors.add(cloneGraph(neighbor));
            }
        }

        return clone;
    }
}
```
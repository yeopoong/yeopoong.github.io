---
layout: post
published: true
title: "1756. Design Most Recently Used Queue"
categories: interview
tags: design binary-search
---

> 가장 최근에 사용한 요소를 대기열의 끝으로 이동시키는 데이터 구조를 설계

- [1756. Design Most Recently Used Queue](https://leetcode.com/problems/design-most-recently-used-queue/)

```java
class MRUQueue {

    Node[] nodes;
    int bucket;
    
    // 가장 최근에 사용된 대기열
    public MRUQueue(int n) {
        bucket = (int) Math.sqrt(n);
        
        nodes = new Node[(n+bucket - 1) / bucket];
        
        Arrays.asList(nodes).replaceAll(i->new Node(-1));
        
        for (int i = 1; i <= n;++i) {
            nodes[(i - 1) / bucket].pre.append(new Node(i));
        }
    }
    
    public int fetch(int k) {
        var ans = nodes[--k/bucket].nxt;
        
        for (int i = k % bucket; i > 0; --i) { //seek to target inside bucket
            ans = ans.nxt;
        }
        
        ans.remove();
        
        for (int i = 1 + k / bucket; i < nodes.length; ++i) { //rebalance
            nodes[i - 1].pre.append(nodes[i].nxt.remove());
        }
        
        nodes[nodes.length - 1].pre.append(ans);
        
        return ans.val;
    }
    
    static class Node {
        Node pre = this, nxt = this;
        
        int val;
        
        Node (int v) {
            val = v;
        }
        
        void append(Node node){
            var tmp = nxt;
            nxt = node;
            node.pre = this;
            node.nxt = tmp;
            tmp.pre = node;
        }
        
        Node remove() {
            pre.nxt = nxt;
            nxt.pre = pre;
            return nxt = pre = this;
        }
    }
}

/**
 * Your MRUQueue object will be instantiated and called as such:
 * MRUQueue obj = new MRUQueue(n);
 * int param_1 = obj.fetch(k);
 */
```

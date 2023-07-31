---
layout: post
published: true
title: "990. Satisfiability of Equality Equations"
categories: interview
tags: medium graph 
---

> 주어진 방정식을 모두 만족시키기 위해 변수 이름에 정수를 할당할 수 있으면 true를 반환하고 그렇지 않으면 false를 반환

[990. Satisfiability of Equality Equations](https://leetcode.com/problems/satisfiability-of-equality-equations/)

```java
class Solution {
    
    int root[] = new int[26];
    
    // 등식의 만족 가능성: 주어진 방정식을 모두 만족시키는 정수가 있으면 true
    public boolean equationsPossible(String[] equations) {
        
        for (int i = 0; i < 26; i++) {
            root[i] = i;
        }

        for (String eqn : equations) {
            if (eqn.charAt(1) == '=') {
                int x = eqn.charAt(0) - 'a';
                int y = eqn.charAt(3) - 'a';
                union(x, y);
            }
        }

        for (String eqn : equations) {
            if (eqn.charAt(1) == '!') {
                int x = eqn.charAt(0) - 'a';
                int y = eqn.charAt(3) - 'a';
                if (find(x) == find(y))
                    return false;
            }
        }

        return true;
    }

    private int find(int x) {
        if (root[x] != x) {
            root[x] = find(root[x]);
        }
        
        return root[x];
    }

    private void union(int x, int y) {
        x = find(x);
        y = find(y);
        
        if (x != y) {
            root[x] = y;
        }
    }
}
```
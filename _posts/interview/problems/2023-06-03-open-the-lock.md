---
layout: post
published: true
title: "752. Open the Lock"
categories: interview
tags: bfs
---

> 자물쇠를 여는 바퀴의 값을 나타내는 코드가 주어지면 자물쇠를 여는 데 필요한 최소 총 회전 수를 반환

- [752. Open the Lock](https://leetcode.com/problems/open-the-lock/)

```java
class Solution {
    
    // 자물쇠를 여는 바퀴의 값을 나타내는 코드가 주어지면 자물쇠를 여는 데 필요한 최소 총 회전 수를 반환
    public int openLock(String[] deadends, String target) {
        Queue<String> queue = new LinkedList<>();
        queue.add("0000");
        
        Set<String> visited = new HashSet<>(Arrays.asList(deadends));
        
        int depth = -1;
        
        while (!queue.isEmpty()) {
            depth++;
            int size = queue.size();
            for (int i = 0; i < size; i++) {
                String node = queue.poll();
                if (node.equals(target)) return depth;
                if (visited.contains(node)) continue;
                visited.add(node);
                queue.addAll(getSuccessors(node));
            }
        }
        
        return -1;
    }
	
    private List<String> getSuccessors(String str) {
        List<String> res = new LinkedList<>();
        
        for (int i = 0; i < str.length(); i++) {
            res.add(str.substring(0, i) + (str.charAt(i) == '0' ? 9 :  str.charAt(i) - '0' - 1) + str.substring(i+1));
            res.add(str.substring(0, i) + (str.charAt(i) == '9' ? 0 :  str.charAt(i) - '0' + 1) + str.substring(i+1));
        }
        
        return res;
    }
}
```

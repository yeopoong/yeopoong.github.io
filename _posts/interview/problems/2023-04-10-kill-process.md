---
layout: post
published: true
title: "582. Kill Process"
categories: interview
tags: interview bfs tree hashmap
---

> 루트 트리 구조를 형성하는 n개의 프로세스에서 죽이려는 프로세스의 ID를 나타내는 정수 kill이 주어지면 죽일 프로세스의 ID 목록을 반환
> HashMap + Breadth First Search

- [582. Kill Process](https://leetcode.com/problems/kill-process/)

```java
class Solution {
    
    // 죽이려는 프로세스의 ID를 나타내는 정수 kill이 주어지면 죽일 프로세스의 ID 목록을 반환
    // 프로세스가 종료되면 모든 하위 프로세스도 종료
    // T: O(n)
    public List<Integer> killProcess(List<Integer> pid, List<Integer> ppid, int kill) {
        List<Integer> list = new ArrayList<>();
        
        // 자식프로세스 리스트를 맵으로 관리
        HashMap<Integer, List<Integer>> map = new HashMap<>();
        
        for (int i = 0; i < ppid.size(); i++) {
            Integer parent = ppid.get(i);
            Integer child = pid.get(i);
            
            List<Integer> children = map.getOrDefault(parent, new ArrayList<Integer>());
            children.add(child);
            
            map.put(parent, children);
        }
        
        // 자식프로세스를 추적하기 위해 사용
        Queue<Integer> queue = new LinkedList<>();
        queue.add(kill);
        
        while (!queue.isEmpty()) {
            int r = queue.remove();
            list.add(r);
            if (map.containsKey(r)) {
                for (int id: map.get(r)) {
                    queue.add(id);
                }
            }
        }
        
        return list;
    }
}
```
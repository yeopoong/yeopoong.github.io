---
layout: post
published: true
title: "207. Course Schedule"
categories: interview
tags: graph dfs
---

> 수강해야 하는 총 numCourses 과정이 있으며 0에서 numCourses - 1까지 레이블이 지정
> This problem is equivalent to finding the topological order in a directed graph.
> If a cycle exists, no topological ordering exists and therefore it will be impossible to take all courses.

- [207. Course Schedule](https://leetcode.com/problems/course-schedule/)

```java
class Solution {
    
    List<List<Integer>> adj = new ArrayList<>();
    
    // all courses along the curr DFS path
    Set<Integer> visited = new HashSet<>();
    
    // 선수과정을 조사해서 모든 코스를 마칠 수 있는지 체크
    // O(n + p)
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        
        // 코스 리스트 생성
        for (int i = 0; i < numCourses; i++) {
            adj.add(new ArrayList<>());
        }

        // 선수과목 데이터 초기화
        for (int i = 0; i < prerequisites.length; i++) {
            adj.get(prerequisites[i][0]).add(prerequisites[i][1]);
        }
        
        // 과목별로 DFS 탐색을 수행
        for (int course = 0; course < numCourses; course++) {
            if (!dfs(course)) {
                return false;
            }
        }
        
        return true;
    }

    // DFS
    private boolean dfs(int course) {
        // detected a loop
        if (visited.contains(course)) {
            return false;
        }
        
        List<Integer> list = adj.get(course);
        
        // 선수과정이 없을 경우
        if (list.size() == 0) {
            return true;
        }

        visited.add(course);
        // 선수과목을 DFS 탐색한다.
        for (Integer pre : list) {
            if (!dfs(pre)) {
                return false;
            }
        }
        visited.remove(course);
        
        // * 방문한 과목은 더 이상 처리하지 않도록 한다.
        list.clear(); 
        
        return true;
    }
}
```

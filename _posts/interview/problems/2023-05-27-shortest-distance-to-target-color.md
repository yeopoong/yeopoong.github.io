---
layout: post
published: true
title: "1182. Shortest Distance to Target Color"
categories: interview
tags: linked-list two-pointers
---

> 1, 2, 3의 세 가지 색상이 있는 배열에서 주어진 인덱스 i와 대상 색상 c 사이의 최단 거리를 반환

- [1182. Shortest Distance to Target Color](https://leetcode.com/problems/shortest-distance-to-target-color/)

```java
class Solution {
    
    // 대상 색상까지의 최단 거리
    public List<Integer> shortestDistanceColor(int[] colors, int[][] queries) {
        List<Integer> result = new ArrayList<>();
        
        Map<Integer, List<Integer>> map = new HashMap<>();

        // 색상별로 인덱스 리스트를 저장한다.
        for (int i = 0; i < colors.length; i++) {
            map.putIfAbsent(colors[i], new ArrayList<Integer>());
            map.get(colors[i]).add(i);
        }

        // 쿼리를 처리한다.
        for (int i = 0; i < queries.length; i++) {
            int target = queries[i][0], color = queries[i][1];
            
            if (!map.containsKey(color)) {
                result.add(-1);
                continue;
            }

            // 색상의 인덱스 리스트를 구한다.
            List<Integer> indexList = map.get(color);
            int insert = Collections.binarySearch(indexList, target);

            // due to its nature, we need to convert the returning values
            // from Collections.binarySearch
            // more details: https://docs.oracle.com/en/java/javase/12/docs/api/java.base/java/util/Collections.html#binarySearch(java.util.List,T)
            if (insert < 0) {
                insert = (insert + 1) * -1;
            }

            // Handling cases when:
            // - the target index is smaller than all elements in the indexList
            // - the target index is larger than all elements in the indexList
            // - the target index sits between the left and right boundaries
            if (insert == 0) {
                result.add(indexList.get(insert) - target);
            } else if (insert == indexList.size()) {
                result.add(target - indexList.get(insert - 1));
            } else {
                int leftNearest = target - indexList.get(insert - 1);
                int rightNearest = indexList.get(insert) - target;
                result.add(Math.min(leftNearest, rightNearest));
            }

        }
        
        return result;
    }
}
```
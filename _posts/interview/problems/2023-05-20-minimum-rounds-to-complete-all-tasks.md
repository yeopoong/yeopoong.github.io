---
layout: post
published: true
title: "2390. Removing Stars From a String"
categories: interview
tags: problems array greedy
---

> 모든 작업을 완료하기 위한 최소 라운드
> - tasks[i]는 작업의 난이도를 나타냅니다.  
> - 각 라운드에서 동일한 난이도의 작업을 2개 또는 3개 완료할 수 있습니다.  

- [2244. Minimum Rounds to Complete All Tasks](https://leetcode.com/problems/minimum-rounds-to-complete-all-tasks/)

```java
class Solution {
    
    // Greedy
    // 모든 작업을 완료하는 데 필요한 최소 라운드
    // 각 라운드에서 동일한 난이도의 작업을 2개 또는 3개 완료할 수 있다.
    // T: O(n)
    public int minimumRounds(int[] tasks) {
        int minimumRounds = 0;
        
        Map<Integer, Integer> freq = new HashMap();
        
        // Store the frequencies in the map.
        for (int task : tasks) {
            freq.put(task, freq.getOrDefault(task, 0) + 1);
        }

        // Iterate over the task's frequencies.
        for (int count : freq.values()) {
            // If the frequency is 1, it's not possible to complete tasks.
            if (count == 1) {
                return - 1;
            }

            if (count % 3 == 0) {
                // Group all the task in triplets.
                minimumRounds += count / 3;
            } else {
                // If count % 3 = 1; 2 / 3 + 1 = 1 
                // If count % 3 = 2; 5 / 3 + 1 = 2 
                minimumRounds += count / 3 + 1;
            }
        }

        return minimumRounds;
    }
}
```
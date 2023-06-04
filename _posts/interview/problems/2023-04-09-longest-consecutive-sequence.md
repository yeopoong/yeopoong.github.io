---
layout: post
published: true
title: "128. Longest Consecutive Sequence"
categories: interview
tags: hashmap array
---

> 정렬되지 않은 정수 배열이 주어지면 가장 긴 연속 시퀀스의 길이를 반환

- [128. Longest Consecutive Sequence](https://leetcode.com/problems/longest-consecutive-sequence/)

```java
class Solution {
    // 가장 긴 연속 시퀀스
    // 맵에서 이전값과 다음값이 존재하는지 체크하면서 최대길이를 증가 시킨다.
    // T: O(n), S: O(n)
    public int longestConsecutive(int[] nums) {
        int longest = 0;
        
        Set<Integer> set = new HashSet<>();
        for (int num : nums) {
            set.add(num);
        }

        for (int num : set) {
            // 현재 번호 바로 앞에 오는 번호가 반드시 더 긴 시퀀스의 일부여야 하므로 먼저 존재하지 않는지 확인
            if (!set.contains(num-1)) {
                // 연속값 초기화
                int length = 1;

                // 다음 숫자가 존재할때까지 반복한다. 
                while (set.contains(num + length)) {
                    length++;
                }

                // 기존의 결과와 비교해서 더 크면 갱신
                longest = Math.max(longest, length);
            }
        }

        return longest;
    }
}
```
---
layout: post
published: false
title: "Sliding Window"
categories: interview
tags: interview 
---

## Sliding Window

[Medium]
- [53. Maximum Subarray](https://leetcode.com/problems/maximum-subarray/)
- [209. Minimum Size Subarray Sum](https://leetcode.com/problems/minimum-size-subarray-sum/)
- [239. Sliding Window Maximum](https://leetcode.com/problems/sliding-window-maximum/)
- [325. Maximum Size Subarray Sum Equals k](https://leetcode.com/problems/maximum-size-subarray-sum-equals-k/)
- [1151. Minimum Swaps to Group All 1's Together](https://leetcode.com/problems/minimum-swaps-to-group-all-1s-together/)
- [159. Longest Substring with At Most Two Distinct Characters](https://leetcode.com/problems/longest-substring-with-at-most-two-distinct-characters/)
```java
class Solution {
    
    // 최대 두 개의 개별 문자를 포함하는 가장 긴 하위 문자열의 길이
    // T: O(n)
    public int lengthOfLongestSubstringTwoDistinct(String s) {
        int longest = 1;
        
        int n = s.length();

        // sliding window left and right pointers
        int left = 0, right = 0;
        
        // 문자와 인덱스를 저장한다.
        HashMap<Character, Integer> map = new HashMap<>();

        while (right < n) {
            // 문자를 맵에 넣는다. 
            map.put(s.charAt(right), right++);

            // 맵에 문자가 3개가 되면 가장 왼쪽 문자를 지운다. 
            if (map.size() == 3) {
                // 값중에서 최소값을 찾는다. 
                left = Collections.min(map.values());
                // 해당 위치의 문자를 맵에서 지운다.
                map.remove(s.charAt(left));
                left += 1;
            }

            longest = Math.max(longest, right - left);
        }
        
        return longest;
    }
}
```
- [340. Longest Substring with At Most K Distinct Characters](https://leetcode.com/problems/longest-substring-with-at-most-k-distinct-characters/)

[Hard]
- [239. Sliding Window Maximum](https://leetcode.com/problems/sliding-window-maximum/)
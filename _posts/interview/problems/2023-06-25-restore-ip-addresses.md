---
layout: post
published: true
title: "93. Restore IP Addresses"
categories: interview
tags: medium backtracking
---

> 숫자만 포함된 문자열 s가 주어지면 s에 점을 삽입하여 형성할 수 있는 가능한 모든 유효한 IP 주소를 반환

[93. Restore IP Addresses](https://leetcode.com/problems/restore-ip-addresses/)

```java
class Solution {
    
    List<String> solutions = new ArrayList<String>();
    
    // T: O(3^n)
    public List<String> restoreIpAddresses(String s) {
        restoreIp(s, 0, "", 0);
        return solutions;
    }

    private void restoreIp(String ip, int idx, String restored, int count) {
        if (count > 4) return;
        
        if (count == 4 && idx == ip.length()) {
            solutions.add(restored);
        } 

        for (int i = 1; i < 4; i++) {
            if (idx+i > ip.length()) {
                break;
            }
            
            String s = ip.substring(idx, idx + i);
            
            if ((s.startsWith("0") && s.length() > 1) || (i == 3 && Integer.parseInt(s) >= 256)) {
                continue;
            }
            
            restoreIp(ip, idx + i, restored + s + (count == 3 ? "" : "."), count + 1);
        }
    }
}
}
```

---
layout: post
published: true
title: "451. Sort Characters By Frequency"
categories: interview
tags: problems union-find graph dfs
---

> 문자열 s가 주어지면 문자 빈도에 따라 내림차순으로 정렬

- [721. Accounts Merge](https://leetcode.com/problems/accounts-merge/)

```java
class Solution {
    
    Map<String, String> parents = new HashMap<>();
    
    // 계정 병합: 두 계정에 공통 이메일이 있는 경우 두 계정은 같은 사람에게 속합니다.
    public List<List<String>> accountsMerge(List<List<String>> accounts) {
        List<List<String>> res = new ArrayList<>();
        
        Map<String, String> owner = new HashMap<>();
        Map<String, TreeSet<String>> unions = new HashMap<>();
        
        for (List<String> a : accounts) {
            for (int i = 1; i < a.size(); i++) {
                parents.put(a.get(i), a.get(i));
                owner.put(a.get(i), a.get(0));
            }
        }
        
        for (List<String> a : accounts) {
            String p = find(a.get(1));
            for (int i = 2; i < a.size(); i++)
                parents.put(find(a.get(i)), p);
        }
        
        for (List<String> a : accounts) {
            String p = find(a.get(1));
            if (!unions.containsKey(p)) unions.put(p, new TreeSet<>());
            for (int i = 1; i < a.size(); i++)
                unions.get(p).add(a.get(i));
        }
        
        for (String p : unions.keySet()) {
            List<String> emails = new ArrayList(unions.get(p));
            emails.add(0, owner.get(p));
            res.add(emails);
        }
        
        return res;
    }
    
    private String find(String s) {
        return (parents.get(s) == s) ? s : find(parents.get(s));
    }
}
```

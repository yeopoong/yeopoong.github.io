---
layout: post
published: true
title: "937. Reorder Data in Log Files"
categories: interview
tags: medium sort
---

> 공백으로 구분되고 문자와 숫자로 구성된 문자열 로그 배열을 정렬

[937. Reorder Data in Log Files](https://leetcode.com/problems/reorder-data-in-log-files/)

```java
class Solution {
    public String[] reorderLogFiles(String[] logs) {
       List<String> digi = new ArrayList<>();
        List<String> word = new ArrayList<>();
        
        for (String s: logs) {
            if (Character.isDigit(s.charAt(s.length()-1)))
                digi.add(s);
            else
                word.add(s);
        }
        
        Collections.sort(word, new Comparator<String>() {
            public int compare(String s1, String s2) {
                int firstSpacePosition = s1.indexOf(" ");
                String firstWord = s1.substring(firstSpacePosition, s1.length());
                
                int secondSpacePosition = s2.indexOf(" ");
                String secondWord = s2.substring(secondSpacePosition, s2.length());
                
                if (firstWord.compareTo(secondWord) == 0) {
                    firstWord = s1.substring(0, firstSpacePosition);
                    secondWord = s2.substring(0, secondSpacePosition);
                }
                
                return firstWord.compareTo(secondWord);
            }
        });

        String result[] = new String[digi.size() + word.size()];
        int index = 0;

        for (String s: word) result[index++] = s;
        for (String s: digi) result[index++] = s;

        return result;
    }
}
```
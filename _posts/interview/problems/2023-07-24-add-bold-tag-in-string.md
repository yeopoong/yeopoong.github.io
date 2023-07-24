---
layout: post
published: true
title: "616. Add Bold Tag in String"
categories: interview
tags: medium interval
---

> 문자열과 문자열 배열이 주어지면, 문자열 배열의 단어가 문자열의 서브스트링에 존재하면 해당 부분을 볼드 태그로 감싼다.

[616. Add Bold Tag in String](https://leetcode.com/problems/add-bold-tag-in-string/)

```java
class Solution {
    
    public String addBoldTag(String s, String[] words) {
        List<Interval> intervals = new ArrayList<>();
        for (String str : words) {
        	int index = -1;
        	index = s.indexOf(str, index);
        	while (index != -1) {
        		intervals.add(new Interval(index, index + str.length()));
        		index +=1;
        		index = s.indexOf(str, index);
        	}
        }
        System.out.println(Arrays.toString(intervals.toArray()));
        intervals = merge(intervals);
        System.out.println(Arrays.toString(intervals.toArray()));
        int prev = 0;
        StringBuilder sb = new StringBuilder();
        for (Interval interval : intervals) {
        	sb.append(s.substring(prev, interval.start));
        	sb.append("<b>");
        	sb.append(s.substring(interval.start, interval.end));
        	sb.append("</b>");
        	prev = interval.end;
        }
        if (prev < s.length()) {
        	sb.append(s.substring(prev));
        }
        return sb.toString();
    }
	
	class Interval {
		int start, end;
		public Interval(int s, int e) {
			start = s;
			end = e;
		}
		
		public String toString() {
			return "[" + start + ", " + end + "]" ;
		}
	}
	
	public List<Interval> merge(List<Interval> intervals) {
        if (intervals == null || intervals.size() <= 1) {
            return intervals;
        }
        Collections.sort(intervals, new Comparator<Interval>(){
            public int compare(Interval a, Interval b) {
                return a.start - b.start;
            }
        });
        
        int start = intervals.get(0).start;
        int end = intervals.get(0).end;
        List<Interval> res = new ArrayList<>();
        for (Interval i : intervals) {
            if (i.start <= end) {
                end = Math.max(end, i.end);
            } else {
                res.add(new Interval(start, end));
                start = i.start;
                end = i.end;
            }
        }
        res.add(new Interval(start, end));
        return res;
    }
}
```
---
layout: post
published: true
title: "729. My Calendar I"
categories: interview
tags: problems design interval
---

> 달력으로 사용할 프로그램을 구현하고 있습니다. 이벤트를 추가해도 이중 예약이 발생하지 않는 경우 새 이벤트를 추가

- [729. My Calendar I](https://leetcode.com/problems/my-calendar-i/)

```java
class MyCalendar {

    List<int[]> calendar;
    
    public MyCalendar() {
        this.calendar = new ArrayList<>();
    }
    
    // T: O(n)
    public boolean book(int start, int end) {
        // 중복 체크: 둘 중 하나가 다른 하나가 끝난 후에 시작하는 경우에만 충돌하지 않는다.
        for (int[] cal: calendar) {
            if (cal[0] < end && start < cal[1]) return false;
        }
        
        // 신규 이벤트 저장
        calendar.add(new int[] {start, end});
        return true;
    }
}

/**
 * Your MyCalendar object will be instantiated and called as such:
 * MyCalendar obj = new MyCalendar();
 * boolean param_1 = obj.book(start,end);
 */
```

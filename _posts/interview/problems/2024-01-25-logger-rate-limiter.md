---
layout: post
published: true
title: "359. Logger Rate Limiter"
categories: interview
tags: easy hashmap
---

> 타임스탬프와 함께 메시지 스트림을 수신하는 로거 시스템을 설계, 각 고유 메시지는 최대 10초마다 인쇄되어야 함

[359. Logger Rate Limiter](https://leetcode.com/problems/logger-rate-limiter/)

```java
class Logger {
    
    private final HashMap<String, Integer> map;
    //private final Object lock;
	
    public Logger() {
    	map = new HashMap<>();
    	//lock = new Object();
    }
    
    // 각각의 고유한 메시지는 최대 10초마다 인쇄
    // 여러 메시지가 동일한 타임스탬프에 도착할 수 있다 -> 동기화가 필요한다.
    // T: O(1), S: O(M)
    public boolean shouldPrintMessage(int timestamp, String message) {
        Integer ts = map.get(message);
        // 메시지가 없거나 10초보다 오래됬으면 갱신한다.
        if (ts == null || timestamp - ts >= 10) {
        	//synchronized (lock) {
        		//Integer ts2 = map.get(message);
        		//if (ts == null || timestamp - ts2 >= 10) {
		            map.put(message, timestamp);
        			return true;
        		//}
        	//}
         } 

        return false;
    }
}
```
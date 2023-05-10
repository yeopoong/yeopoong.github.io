---
layout: post
published: true
title: "1114. Print in Order"
categories: interview
tags: problems concurrency design
---

> first() 다음에 second()가 실행되고 second() 다음에 third()가 실행되도록 메커니즘을 설계하고 프로그램을 수정  
> - Problems of Concurrency

- [1114. Print in Order](https://leetcode.com/problems/print-in-order/)

```java
class Foo {
    
    private AtomicInteger firstJobDone = new AtomicInteger(0);
    private AtomicInteger secondJobDone = new AtomicInteger(0);

    public Foo() {
        
    }

    public void first(Runnable printFirst) throws InterruptedException {
        
        // printFirst.run() outputs "first". Do not change or remove this line.
        printFirst.run();
        // mark the first job as done, by increasing its count.
        firstJobDone.incrementAndGet();
    }

    public void second(Runnable printSecond) throws InterruptedException {
        
        while (firstJobDone.get() != 1) {
            // waiting for the first job to be done.
        }
        
        // printSecond.run() outputs "second". Do not change or remove this line.
        printSecond.run();
        
        // mark the second as done, by increasing its count.
        secondJobDone.incrementAndGet();
    }

    public void third(Runnable printThird) throws InterruptedException {
        while (secondJobDone.get() != 1) {
            // waiting for the second job to be done.
        }
        
        // printThird.run() outputs "third". Do not change or remove this line.
        printThird.run();
    }
}
```

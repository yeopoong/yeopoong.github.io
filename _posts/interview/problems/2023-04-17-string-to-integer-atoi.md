---
layout: post
published: true
title: "8. String to Integer (atoi)"
categories: interview
tags: string
---

> 문자열을 부호 있는 32비트 정수로 변환하는 myAtoi(string s) 함수를 구현

- [8. String to Integer (atoi)](https://leetcode.com/problems/string-to-integer-atoi/)

```java
class Solution {
    
    // T: O(n), S: O(1)
    public int myAtoi(String str) {
        int sign = 1, total = 0;
        
        int index = 0;
        int length = str.length();

        //1. Empty string
        if (length == 0) return 0;
    
        //2. Remove leading whitespaces
        while (index < length && str.charAt(index) == ' ') index++;
    
        //3. Handle signs
        if (index < length && (str.charAt(index) == '+' || str.charAt(index) == '-')) {
            sign = (str.charAt(index) == '+') ? 1 : -1;
            index++;
        }
        
        //4. Convert number and avoid overflow
        while (index < length && Character.isDigit(str.charAt(index))) {
            int digit = str.charAt(index) - '0';

            //check if total will be overflow after 10 times
            //2147483647: 214748364 = (INT_MAX / 10)
            if (Integer.MAX_VALUE/10 < total || (Integer.MAX_VALUE/10 == total && Integer.MAX_VALUE %10 < digit)) {
                return sign == 1 ? Integer.MAX_VALUE : Integer.MIN_VALUE;
            }

            //append current digit to the result
            total = 10 * total + digit;
            index++;
        }

        return total * sign;
    }
}
```

Deterministic Finite Automaton (DFA)

```java
enum State { q0, q1, q2, qd }

class StateMachine {
    // Store current state value.
    private State currentState;
    // Store result formed and it's sign.
    private int result, sign;

    public StateMachine() {
        currentState = State.q0;
        result = 0;
        sign = 1;
    }

    // Transition to state q1.
    private void toStateQ1(char ch) {
        sign = (ch == '-') ? -1 : 1;
        currentState = State.q1;
    }

    // Transition to state q2.
    private void toStateQ2(int digit) {
        currentState = State.q2;
        appendDigit(digit);
    }

    // Transition to dead state qd.
    private void toStateQd() {
        currentState = State.qd;
    }

    // Append digit to result, if out of range return clamped value.
    private void appendDigit(int digit) {
        if ((result > Integer.MAX_VALUE / 10) || 
            (result == Integer.MAX_VALUE / 10 && digit > Integer.MAX_VALUE % 10)) {
            if (sign == 1) {
                // If sign is 1, clamp result to Integer.MAX_VALUE.
                result = Integer.MAX_VALUE;
            } else {
                // If sign is -1, clamp result to Integer.MIN_VALUE.
                result = Integer.MIN_VALUE;
                sign = 1;
            }

            // When the 32-bit int range is exceeded, a dead state is reached.
            toStateQd();
        } else {
            // Append current digit to the result. 
            result = result * 10 + digit;
        }
    }

    // Change state based on current input character.
    public void transition(char ch) {
        if (currentState == State.q0) {
            // Beginning state of the string (or some whitespaces are skipped).
            if (ch == ' ') {
                // Current character is a whitespaces.
                // We stay in same state. 
                return;
            } else if (ch == '-' || ch == '+') {
                // Current character is a sign.
                toStateQ1(ch);
            } else if (Character.isDigit(ch)) {
                // Current character is a digit.
                toStateQ2(ch - '0');
            } else {
                // Current character is not a space/sign/digit.
                // Reached a dead state.
                toStateQd();
            }
        } else if (currentState == State.q1 || currentState == State.q2) {
            // Previous character was a sign or digit.
            if (Character.isDigit(ch)) {
                // Current character is a digit.
                toStateQ2(ch - '0');
            } else {
                // Current character is not a digit.
                // Reached a dead state.
                toStateQd();
            }
        }
    }
    
    // Return the final result formed with it's sign.
    public int getInteger() {
        return sign * result;
    }

    // Get current state.
    public State getState() {
        return currentState;
    }
};

class Solution {
    public int myAtoi(String s) {
        StateMachine Q = new StateMachine();
        
        for (int i = 0; i < s.length() && Q.getState() != State.qd; ++i) {
            Q.transition(s.charAt(i));
        }
        
        return Q.getInteger();
    }
}
```
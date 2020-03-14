---
title: LeetCode小試身手
date: 2020/02/10 15:51:50
categories:
- 宅宅工程師
tags:
- leetcode
- c#
---

## What Program Language?
Top 5 best programming languages for 2020 by [TIOBE](https://www.tiobe.com/tiobe-index/)
1. Java
2. C
3. Python
4. C++
5. C#

## Why LeetCode?
~~solve interview questions~~
improve coding skills!


## Question
[[Easy] 1342. Number of Steps to Reduce a Number to Zero](https://leetcode.com/problems/number-of-steps-to-reduce-a-number-to-zero/)

```
Input: num = 14
Output: 6

Explanation:
Step 1) 14 is even; divide by 2 and obtain 7.
Step 2) 7 is odd; subtract 1 and obtain 6.
Step 3) 6 is even; divide by 2 and obtain 3.
Step 4) 3 is odd; subtract 1 and obtain 2.
Step 5) 2 is even; divide by 2 and obtain 1.
Step 6) 1 is odd; subtract 1 and obtain 0.
```

## My Answer
```
// C#.C.C++.Java
public class Solution
{
    public int NumberOfSteps (int num)
    {
        if(0==num)
        {
            return 0;
        }
        else if(0==num%2)
        {
            return 1 + NumberOfSteps(num/2);
        }
        else
        {
            return 1 + NumberOfSteps(num-1);
        }
    }
}

// Python
class Solution(object):
    def numberOfSteps (self, num):
        """
        :type num: int
        :rtype: int
        """

        if num == 0:
            return 0

        if num%2 == 0:
            return 1 + self.numberOfSteps(num/2)
        else:
            return 1 + self.numberOfSteps(num-1)
```

## Best Answer👍
```
if(!num) return 0;
int res = 0;
while(num) {
    res += (num & 1) ? 2 : 1;
    num >>= 1;
}
return res - 1;
```
For the binary representation from left to right:
if we meet 0, result += 1 because num/2.
if we meet 1, result += 2 because num-1 then num/2.
exception leftmost 1, we just do num-1.

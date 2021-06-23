---
layout: posts
title:  "[LeetCode] Climbing Stairs"
categories: ['Algorithm', 'LeetCode']
---


[문제링크]:(https://leetcode.com/problems/climbing-stairs/)





Easy

You are climbing a staircase. It takes `n` steps to reach the top.

Each time you can either climb `1` or `2` steps. In how many distinct ways can you climb to the top?

 

**Example 1:**

```
Input: n = 2
Output: 2
Explanation: There are two ways to climb to the top.
1. 1 step + 1 step
2. 2 steps
```

**Example 2:**

```
Input: n = 3
Output: 3
Explanation: There are three ways to climb to the top.
1. 1 step + 1 step + 1 step
2. 1 step + 2 steps
3. 2 steps + 1 step  
```

 

**Constraints:**

- `1 <= n <= 45`





### Sol

지난번 [LeetCode] Unique Path 문제를 풀면서 DP문제를 처음 접하는 분들에게 추천한 문제입니다.

Top까지의 거리를 n으로 주어지고 한번에 1칸 또는 2칸씩 계단을 오를 수 있는 상황에서,

Top에 도달하는 경우의 수를 구하는 문제입니다.  
# 



n=1 인 경우, 1칸 오르면 Top에 도달하므로, 경우의 수는 1 입니다.

n=2 인 경우, 1칸씩 두번 오르거나 2칸을 한번에 오를 수 있으므로, 경우의 수는 2 입니다.  
<br/> 



n=3 인 경우를 봅시다.

한번에 1칸 또는 2칸만 오를 수 있으므로, Top=3에 도달하는 순간에는 무조건

- 1번 계단에서 2칸 올라 3번 계단(Top)에 도달하는 경우 

- 2) 2번 계단에서 1칸 올라 3번 계단(Top)에 도달하는 경우

위 2가지 경우 뿐 입니다.  
<br/> 



즉, 1)에 해당하는 경우의수와 2)에 해당하는 경우의 수의 합으로 n=3인 경우의 수를 구할 수 있습니다.

 	이때 1)과 2)는 각각 앞서 구해둔 n=1인 경우의 수와 n=2인 경우의 수 입니다.  
<br/>   


따라서, 입력된 n에 대한 경우의 수는 다음과 같은 점화식을 따릅니다.

![img](https://github.com/guard1000/guard1000.github.io/blob/master/imgs/%5BLeetCode%5D%20Climbing%20Stairs_1.png?raw=true)

이를 활용하여 다음과 같은 아주 간단한 코드로 문제를 해결할 수 있습니다.  
<br/>



### Code

```python
class Solution:
    def climbStairs(self, n: int) -> int:
        if n == 1 or n == 2:
            return n
        answer = [1,2]
        for _ in range(n-2):
            answer.append(answer[-1] + answer[-2])
        return answer[-1]
    
```


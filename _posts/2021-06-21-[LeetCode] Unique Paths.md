---
layout: posts
title:  "[LeetCode] Unique Paths"
categories: ['Algorithm', 'LeetCode']
---

### [LeetCode] Unique Paths 
[문제링크]:https://leetcode.com/problems/unique-paths/





A robot is located at the top-left corner of a `m x n` grid (marked 'Start' in the diagram below).

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).

How many possible unique paths are there?

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2018/10/22/robot_maze.png)

```
Input: m = 3, n = 7
Output: 28
```

**Example 2:**

```
Input: m = 3, n = 2
Output: 3
Explanation:
From the top-left corner, there are a total of 3 ways to reach the bottom-right corner:
1. Right -> Down -> Down
2. Down -> Down -> Right
3. Down -> Right -> Down
```

**Example 3:**

```
Input: m = 7, n = 3
Output: 28
```

**Example 4:**

```
Input: m = 3, n = 3
Output: 6
```





### Sol

맵의 size가 주어지고 로봇을 Finish로 최단거리로 옮길 수 있는 경우의 수를 구하는 문제입니다.



Example 1 의 m=3, n=7 인 경우,

![img](https://assets.leetcode.com/uploads/2018/10/22/robot_maze.png)

결국 Finish에 도달하기 위해  ↓(down) 2번,  →(right) 6번이 필요합니다.

즉, 이 문제는  [↓, ↓, →, →, →, →, →, →] 를 배치하는 '경우의 수' 문제로 볼 수 있습니다.

중복이 있는 배치 경우의 수 풀이는 다음과 같습니다.

![img](https://github.com/guard1000/guard1000.github.io/blob/master/imgs/%5BLeetCode%5D%20Unique%20Paths_1.png?raw=true)



그럼 이제, m과 n에 대해 일반해를 구할 수 있습니다.

<img src="https://github.com/guard1000/guard1000.github.io/blob/master/imgs/%5BLeetCode%5D%20Unique%20Paths_2.png?raw=true" style="zoom:80%;" />





### Code

```python
import math
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        return int(math.factorial(m+n-2)/(math.factorial(m-1) * math.factorial(n-1)))
```



math 라이브러리의 factorial을 활용했습니다.


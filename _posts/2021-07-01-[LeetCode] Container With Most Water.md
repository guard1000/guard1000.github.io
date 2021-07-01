---
layout: posts
title:  "[LeetCode] Container With Most Water"
categories: ['Algorithm', 'LeetCode']
---

[문제링크](https://leetcode.com/problems/container-with-most-water/)

Given `n` non-negative integers `a1, a2, ..., an` , where each represents a point at coordinate `(i, ai)`. `n` vertical lines are drawn such that the two endpoints of the line `i` is at `(i, ai)` and `(i, 0)`. Find two lines, which, together with the x-axis forms a container, such that the container contains the most water.

**Notice** that you may not slant the container.

 

**Example 1:**

![img](C:\Program Files\Typora\2021-07-01-[LeetCode] Container With Most Water\question_11.jpg)

```
Input: height = [1,8,6,2,5,4,8,3,7]
Output: 49
Explanation: The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7]. In this case, the max area of water (blue section) the container can contain is 49.
```

**Example 2:**

```
Input: height = [1,1]
Output: 1
```

**Example 3:**

```
Input: height = [4,3,2,1,4]
Output: 16
```

**Example 4:**

```
Input: height = [1,2,1]
Output: 2
```

 

**Constraints:**

- `n == height.length`
- `2 <= n <= 10**5`
- `0 <= height[i] <= 10**4`







### Sol

문제를 읽었을때 '음 쉬운데?' 라는 생각이 들 때는 항상 한번 더 의심해 봐야 합니다.

브루트하게 풀고자 하면, 바로 조합을 활용하면 간단히 풀릴 것 같습니다.

실제로 조합을 활용한 코드는 다음과 같겠습니다.

```python
# sol 1 - O(N제곱)
    import itertools
    def maxArea(self, height: List[int]) -> int:
        answer = 0
        idxs = [_ for _ in range(len(height))]
        mycombination = itertools.combinations(idxs, 2)
        for mycomb in mycombination:
            tmp = (mycomb[1]-mycomb[0])*min(height[mycomb[1]], height[mycomb[0]])
            if tmp > answer:
                answer = tmp
        return answer
```



<br/>

하지만 역시 답은 맞출 수 있지만, 문제에서 요구한 시간 복잡도를 만족하진 못합니다.

시간복잡도 N제곱인 위 풀이와 달리, N으로 낮출 수 있는 풀이방법은 바로,

Two Pointers를 활용하는 것 입니다. Two Pointers에 익숙지 않은 분들은 다음 문제들을 연습해 보시면 좋습니다.

[백준 - 두수의합](https://www.acmicpc.net/problem/3273)
<br/>
[백준 - 수들의 합 2](https://www.acmicpc.net/problem/2003)

<br/>

[LeetCode - 3 Sum](https://leetcode.com/problems/3sum)

<br/> 

 ![img](C:\Program Files\Typora\2021-07-01-[LeetCode] Container With Most Water\[LeetCode] Container With Most Water_1.png)

1. 먼저 left와 right를 주어진 height의 처음과 마지막의 index로 선언해 줍니다.

2. 이후, left < right인 조건하에 while문을 돌아주며.

3. 순간마다 left 막대와 right 막대 사이에 담을 수 있는 물의 양을 tmp로 구해줍니다.

   이때, 담을 수 있는 물의 양은 (r-l) * min(height[r], height[l]) 이 될 것입니다.

4. 3번에서 구한 tmp가 지금까지의 answer 보다 크다면, answer를 tmp로 대치해 줍니다.

5. 이제 left와 right를 이동하는데, 막대 높이가 더 낮은 녀석을 한칸 이동시켜주면서 진행합니다.

   (height[l] 가 더 작다면 l += 1, height[r]이 더 작다면 r += 1)

<br/>

실제 문제에서 주어진 Example1 은 각 라운드별로 l, r, tmp, answer이 어떻게 변해가는지

 위 그림을 통해 풀어보았습니다.



이 로직을 활용하여 다음과 같은 아주 간단한 코드로 문제를 해결할 수 있습니다.  
<br/>



### Code

```python
class Solution:
    # sol 2 - two pointers
    def maxArea(self, height: List[int]) -> int:
        answer = 0
        l,r = 0, len(height)-1
        
        while l < r:
            tmp = (r - l) * min(height[l], height[r])
            if tmp > answer:
                answer = tmp
            if height[l] >= height[r]:
                r -= 1
            else:
                l += 1
            
        return answer
    
```


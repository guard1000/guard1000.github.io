---
layout: posts
title:  "[LeetCode] Trapping Rain Water"
categories: ['Algorithm', 'LeetCode']


---

[문제링크](https://leetcode.com/problems/trapping-rain-water)

<br/>

Given `n` non-negative integers representing an elevation map where the width of each bar is `1`, compute how much water it can trap after raining.

 

**Example 1:**

![img](C:\Program Files\Typora\2021-06-30-[LeetCode] Trapping Rain Water\rainwatertrap.png)

```
Input: height = [0,1,0,2,1,0,1,3,2,1,2,1]
Output: 6
Explanation: The above elevation map (black section) is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section) are being trapped.
```

**Example 2:**

```
Input: height = [4,2,0,3,2,5]
Output: 9
```

 

**Constraints:**

- `n == height.length`

- `0 <= n <= 3 * 10**5`

- `0 <= height[i] <= 10**5

  

<br/>

### Sol

물이 얼마나 담기는가를 구하는 문제입니다.

사실 저는 처음엔 스택을 활용하여 단방향으로 완전탐색을 하려 했습니다.

그러나 아쉽게도(?) 테스트 케이스 320개 중 319개를 통과하고 마지막 케이스가 Time Limit에 걸렸네요.ㅎㅎ

Hard 난이도인 만큼 특히 접근 아이디어를 한번 더 고민해볼 필요가 있는 문제였습니다!

<br/>

그래서 다른 방법을 찾아보았습니다.

![image-20210629000716895](C:\Program Files\Typora\2021-06-30-[LeetCode] Trapping Rain Water\[LeetCode] Trapping Rain Water_1.png)

1. 결국 물이 차려면 '좌우가 막혀' 있어야 합니다.

2. 그러면 직사각형 넓이 를 구하는데에 밑변이 1이므로, 획득가능한 물의 높이를 구하여 

   answer에 더해주면 되는데요.

3. 바로 이 높이(h)를 어떻게 구하는가가 핵심이었습니다.

4. 만약 idx=4 인 시점이라고 하면,  지금 위치 기준으로 왼쪽을 보아 가장 높은 벽의 높이(l_top)는 2, 오른쪽을 보면 가장 높은 벽의 높이(r_top)은 3 입니다. 

   따라서 idx 4 위치에서 가장 높게 물을 받을 수 있는 높이는 min(l_top, r_top)인 2 입니다.

   ​    (2를 넘어가면 왼쪽으로 물이 넘치겠죠? )

   그럼 이제 idx 4 위치에서 최대 높이는 알겠으니, 시작하는 높이가 어디부터인지 살펴보면,

      height[idx] = 1 이므로, 결과적으론 idx 4 위치에서는 1부터  2 까지의 높이차 만큼의 물을 획득 가능합니다.

   <br/>

   따라서, idx 위치에서 획득 가능한 물의 양은 다음과 같습니다.

   ```python
   max(min(l_top, r_top) - now_h, 0)
   ```

   <br/>

   위 그림에서 문제에서 제시된 Example1의 상황에서 idx별 어떻게 동작하여 정답을 이끌어내는지

   그 과정을 풀어두었으니, 함께 참고하시면 이해에 도움이 될 것입니다.

   <br/>

   코드는 아래와 같습니다.

   

<br/>

### Code

```python
class Solution:
    def trap(self, height: List[int]) -> int:       
        idx, answer = 0, 0
        while idx < len(height):
            now_h = height[idx]
            l_top = max(height[:idx]) if len(height[:idx]) > 0 else 0
            r_top = max(height[idx+1:]) if len(height[idx+1:]) > 0 else 0
            
            s = max(min(l_top, r_top) - now_h, 0)
            answer += s
            
            idx += 1

        return answer
```


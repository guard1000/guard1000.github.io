---
layout: posts
title:  "[LeetCode] 3Sum"
categories: ['Algorithm', 'LeetCode']
---

[문제링크](https://leetcode.com/problems/3sum/)



Medium

Given an integer array nums, return all the triplets `[nums[i], nums[j], nums[k]]` such that `i != j`, `i != k`, and `j != k`, and `nums[i] + nums[j] + nums[k] == 0`.

Notice that the solution set must not contain duplicate triplets.

 

**Example 1:**

```
Input: nums = [-1,0,1,2,-1,-4]
Output: [[-1,-1,2],[-1,0,1]]
```

**Example 2:**

```
Input: nums = []
Output: []
```

**Example 3:**

```
Input: nums = [0]
Output: []
```

 

**Constraints:**

- `0 <= nums.length <= 3000`
- `-105 <= nums[i] <= 105`





### Sol

주어진 리스트에서 3 수의 합이 0이 되는 경우의 수를 반환하는 문제입니다.

저는 a + b + c = 0 일 경우, a + b = -c 라는 점과 Two Pointers을 활용했습니다.

- Two Pointers에 대해 궁금하신 분들은 쉬운 문제로 다음 두 문제를 추천합니다. 

[백준 - 두수의합]:https://www.acmicpc.net/problem/3273
[ 백준 - 수들의 합 2]: https://www.acmicpc.net/problem/2003

<br/> 

nums = [1,0,1,2,-1,4] 인 경우

각 값을 순회하며 target으로 잡고, target 이외의 두 수의 합 == -target 을 만족하는 녀석들을 잡아냈습니다.

<br/>



![img](https://github.com/guard1000/guard1000.github.io/blob/master/imgs/%5BLeetCode%5D%203Sum_1.png?raw=true)


 위와 같이 입력된 nums를 먼저 sorted_num으로 정렬해 주었습니다. 

이유는 two-pointers를 활용하기 위함입니다.

<br/>



먼저, target = -4인 때를 봅시다.

정렬되어 있는 sorted_num의 가장 큰 두 녀석인 sorted_num[-1]과 sorted_num[-2]의 합(3) 보다도

-target(4)이 더 크므로, -4를 포함한 세 수의 합은 무조건 0보다 작을 것이기 때문에 탐색을 생략합니다.

<br/>



즉,  target = sorted_num[idx] 일 때,  

```python
if sorted_num[idx] + sorted_num[-1] + sorted_num[-2] < 0:
    idx += 1
    continue
```

와 같이 불필요한 탐색은 continue로 생략하였습니다.

<br/>



이후엔 sorted_num[idx+1:] 구간 내의 수 들에 대해

-target == sorted_num[l] + sorted_num[r] 을 만족하는

[sorted_num[idx], sorted_num[l], sorted_num[r]] 을 answer에 append() 해주었습니다.

<br/>



이때 sorted_num의 l(left) 와 r(right)은 다음과 같은 로직으로 처리합니다.

![img](https://github.com/guard1000/guard1000.github.io/blob/master/imgs/%5BLeetCode%5D%203Sum_2.png?raw=true)

이 문제에서는 사실 타겟이 무조건 left 보다 작기 때문에(왼쪽에 위치) 더욱 쉽게 구할 수 있습니다.

</br>



최종 코드는 다음과 같습니다.

 ### Code

```python
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        answer, sorted_num = [], sorted(nums)
        idx = 0
        while idx <= len(nums) - 3:            
            l, r = idx+1, len(nums)-1
            if sorted_num[idx] + sorted_num[-1] + sorted_num[-2] < 0:
                idx += 1
                continue

            while l != r:
                if sorted_num[l] + sorted_num[r] < -sorted_num[idx]:
                    l += 1
                else:
                    if sorted_num[l] + sorted_num[r] == -sorted_num[idx] and [sorted_num[idx], sorted_num[l], sorted_num[r]] not in answer:
                        answer.append([sorted_num[idx], sorted_num[l], sorted_num[r]])
                    r -= 1
            
            idx += 1
            
        return answer
    
```



```

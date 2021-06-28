---
layout: posts
title:  "[LeetCode] First Missing Positive"
categories: ['Algorithm', 'LeetCode']

---

[문제링크](https://leetcode.com/problems/first-missing-positive/)

<br/>

Given an unsorted integer array `nums`, find the smallest missing positive integer.

You must implement an algorithm that runs in `O(n)` time and uses constant extra space.

 

**Example 1:**

```
Input: nums = [1,2,0]
Output: 3
```

**Example 2:**

```
Input: nums = [3,4,-1,1]
Output: 2
```

**Example 3:**

```
Input: nums = [7,8,9,11,12]
Output: 1
```

 

**Constraints:**

- `1 <= nums.length <= 5 * 105`
- `-231 <= nums[i] <= 231 - 1`



<br/>

### Sol

리트코드 Top 100 Interview 문제 중 Hard 난이도 문제였습니다.

항상 느끼는 거지만, 리트코드의 문제들은 얼마나 더 빠르고 효율적으로 푸느냐에따라 큰 차이가 있고,

저처럼 설렁설렁 패스만 할 정도로 푸는것에는 그래도 관대하다는(?) 느낌을 받습니다.

<br/>

이 문제는 딱 보자마자 Heap을 사용해야겠구나 라는 생각이 들었습니다.

이분탐색 문제를 풀면서 한번 주절주절 언급드린 적이 있는데, 저는 코테준비를 한참 하던 시절에

항상 Time Limit에 발목을 잡히곤 했습니다. 

그리고 '이분탐색, 스택, 힙, DP'는 그 당시 코테만 보면 탈락의 고배를 마셨었던 저에게 

정말 유용한 무기가 되어주었습니다.

  <br/>

특히 이 문제처럼 O(n) 이라는 빡빡한 Time Complexity를 요구하는 문제는 꼭 '힙'을 떠올리시면 좋습니다.

파이썬의 경우 힙을 활용하기 너무나 좋은 heapq라는 라이브러리가 있으므로 더할나위 없겠죠.



<br/>

힙을 활용한 문제를 더 연습하고 싶은 분들에겐 프로그래머스 코딩테스트 고득점 Kit의 힙 문제들을 추천합니다!

(조만간 고득점 Kit 문제들도 모두 다루겠습니다.)

[프로그래머스-더 맵게](https://programmers.co.kr/learn/courses/30/lessons/42626)

[프로그래머스-디스크 컨트롤러](https://programmers.co.kr/learn/courses/30/lessons/42627)

[프로그래머스-이중우선순위큐](https://programmers.co.kr/learn/courses/30/lessons/42628)



<br/>

![image-20210629000716895](C:\Program Files\Typora\2021-06-29-[LeetCode] First Missing Positive\image-20210629000716895.png)

문제 풀이는 위 사진 한장으로 설명됩니다.

1. 먼저 입력된 nums의 중복을 제거해 줍니다. 

2. 리스트 nums를 heapq의 heapify 함수로 최소힙으로 변환해 줍니다. 

3. nums내의 0 이하의 수들은 불필요하므로 heappop()을 사용해 제거해 줍니다.

   최소힙이므로, heappop()을 하면 가장 작은 값이 제거 됩니다.

4. answer = 1 로 선언해 줍니다.

5. 이제 answer == nums[0]  (nums의 최솟값 <- 최소힙이기 때문)  조건을 만족하는 한

   answer += 1 과 heappop() 을 반복해 줍니다

=> 5번의 loop가 끝나면, answer를 정답으로 반환합니다.

<br/>

위 그림의 오른쪽에는 이해를 돕기 위해 문제의 Example2가 각 단계별 어떻게 돌아가 답을 내는지를 확인할 수 있습니다.

로직이 단계별로 어떻게 동작하는지를 따라가며 이해해 봅시다.

<br/>

참고로, heapq 라이브러리의 사용한 함수별 Time Complexity는 다음과 같습니다.

- heapify()  -> O(N)
- heappop() -> O(logN)



<br/>

### Code

```python
import heapq
class Solution:
    def firstMissingPositive(self, nums: List[int]) -> int:
        nums = list(set(nums))
        heapq.heapify(nums)
        while len(nums) != 0 and nums[0] <= 0:
            heapq.heappop(nums)
        
        answer = 1
        while len(nums) != 0 and answer == nums[0]:
            heapq.heappop(nums)
            answer += 1
        return answer
```

